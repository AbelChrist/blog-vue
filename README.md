# blog-vue
> My simple repository learn Laravel and VueJs (Blog app).

## Built With
- [Laravel 8](https://laravel.com/) - PHP Framework (Controller, Model, API, etc).
- [VueJs](https://vuejs.org/) - JavaScript Framework (Fetch API and View Component).
- [Bootstrap 4.5](https://getbootstrap.com) - CSS Framework (Styling).

## Getting Started
Follow these instructions to run this project on your computer.

### Prerequisites
1. Install PHP and MySQL or install [XAMPP](https://www.apachefriends.org/download.html) (included PHP & MySQL).
2. Install Composer [getcomposer.org](https://getcomposer.org/download/).
3. Install NodeJs [nodejs.org](https://nodejs.org/en/).

### Installation

1. **Clone the repo**.
```bash
git clone https://github.com/abelchrist/blog-vue.git
cd blog-vue
composer install
npm install && npm run dev
copy .env.example .env
```

2. **Configure database.** In ```.env``` file.
```
DB_PORT=3306
DB_DATABASE=blog_vue
DB_USERNAME=root
DB_PASSWORD=
```

3. **Generate key and migrate table.**
```bash
php artisan key:generate
php artisan migrate
php artisan db:seed
```

4. **Run website.**
```bash
php artisan serve
```
And open [http://127.0.0.1:8000](http://127.0.0.1:8000).

## Usage


### API Endpoints

- #### List all articles.
```
GET /api/articles
```

- #### Get an article.
```
GET /api/article/{id}
```

- #### Add an article.
```
POST /api/article
```

- #### Update an article.
```
PATCH /api/article/{id}
```

- #### Delete an article.
```
DELETE /api/article/{id}
```

## Contributing
Any good contributions you make for this project are greatly appreciated.
1. Fork the project.
2. Create your feature branch (```git checkout -b feature/NiceFeature```).
3. Commit your changes (```git commit -m 'Add some Nice Feature'```).
4. Push to the branch (```git push origin feature/NiceFeature```).
5. Open a pull request.

## Author & Contributor
- **[Abel](https://github.com/AbelChrist)** - Project Author.

## License
- Distributed under [MIT license](https://opensource.org/licenses/MIT).
