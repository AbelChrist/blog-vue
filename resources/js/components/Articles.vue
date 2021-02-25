<template>
	<div>
		<h2>Articles</h2>
		<hr>
		<form @submit.prevent="addArticle()" class="mb-3">
			<div class="form-group">
				<input type="text" class="form-control" placeholder="Title" v-model="article.title">
			</div>
			<div class="form-group">
				<textarea class="form-control" placeholder="Body" v-model="article.body"></textarea>
			</div>
			<button type="submit" class="btn btn-light">Save</button>
		</form>
		<hr>
		<nav>
		  <ul class="pagination">
		    <li v-bind:class="[{disabled: !pagination.prev}]" class="page-item">
		    	<a class="page-link" href="#" @click="fetchArticles(pagination.prev)">Previous</a>
		    </li>
		    <li class="page-item disabled">
		    	<a href="#" class="page-link text-dark">{{ pagination.current_page }} of {{ pagination.last_page }}</a>
		    </li>
		    <li v-bind:class="[{disabled: !pagination.next}]" class="page-item"><a class="page-link" href="#" @click="fetchArticles(pagination.next)">Next</a></li>
		  </ul>
		</nav>
		<section class="card mb-2" v-for="article in articles" v-bind:key="article.id">
			<article class="card-body">
				<h3>{{ article.title }}</h3>
				<p>{{ article.body }}</p>
				<hr>
				<button @click="deleteArticle(article.id)"  class="btn btn-danger card-link">Delete</button>
				<button @click="editArticle(article)"  class="btn btn-warning card-link">Edit</button>
			</article>
		</section>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				articles: [],
				article: {
					id: '',
					title: '',
					body: '',
				},
				article_id: '',
				pagination: {},
				edit: false
			}
		},

		created() {
			this.fetchArticles();
		},

		methods: {
			fetchArticles(page_url) {
				let vm = this;
				page_url = page_url || '/api/articles';
				fetch(page_url)
				.then(res => res.json())
				.then(res => {
					this.articles = res.data;
					vm.makePagination(res.meta, res.links);
				})
				.catch(err => console.log(err));
			},

			makePagination(meta, links) {
				let { current_page, last_page} = meta;
				let { next, prev } = links;
				let pagination = {
					current_page,
					last_page,
					next,
					prev
				};
				this.pagination = pagination;
			},

			deleteArticle(id) {
				if(confirm('Are You Sure?')) {
					fetch(`/api/article/${id}` , {method: 'delete'})
					.then(res => res.json())
					.then(res => {
						alert(`Article has been removed!`);
						this.fetchArticles();
					})
					.catch(err => console.log(err));
				}
			},

			addArticle() {
				if(this.edit === false) {
					// Add
					fetch('/api/article', {
						method: 'post',
						body: JSON.stringify(this.article),
						headers: {
							'content-type': 'application/json'
						}
					})
					.then(res => res.json())
					.then(res => {
						this.article.title = '';
						this.article.body = '';
						alert(`Article added!`);
						this.fetchArticles();
					})
					.catch(err => console.log(err));
				} else {
					// Edit
					fetch(`/api/article/${this.article.id}`, {
						method: 'PATCH',
						body: JSON.stringify(this.article),
						headers: {
							'content-type': 'application/json'
						}
					})
					.then(res => res.json())
					.then(res => {
						this.article.title = '';
						this.article.body = '';
						alert(`Article updated!`);
						this.fetchArticles();
						this.edit = false;
					})
					.catch(err => console.log(err));
				}
			},

			editArticle(article) {
				this.edit = true;
				this.article.id = article.id;
				this.article.title = article.title;
				this.article.body = article.body;
			}
		}
	};
</script>
