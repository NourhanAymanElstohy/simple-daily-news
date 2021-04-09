## About Project

This Project is a simple Daily News from 3 agencies using laravel, VueJs and MongoDB

## Packages Used

-   laravel/ui
-   jenssegers/mongodb
-   bootstrap-vue
-   vue-axios

## Tech/framework used

<b>Built with</b>

-   [Laravel](https://laravel.com)
-   [VueJs](https://cli.vuejs.org)

## Features

-   show daily news from 3 agencies
-   sort news of each agency by rating or Date Time

## Installation

Please check the official laravel installation guide for server requirements before you start. [Official Documentation](https://laravel.com/docs/7.x/installation#installation)

Clone the repository

```
git clone https://github.com/NourhanAymanElstohy/simple-daily-news.git
```

Switch to the repo folder

```
cd simple-daily-news
```

Install all the dependencies using composer and npm

```
composer install
npm install
```

Copy the example env file and make the required configuration changes in the .env file

```
cp .env.example .env
```

Generate a new application key

```
php artisan key:generate
```

## Database

Download Database from [Database Zip File](https://drive.google.com/file/d/1qiMrhcwnFEY6fZU_RpBV-a1OQHYZhbxb/view?usp=sharing) Then extract it

Import Database

```
mongorestore --host localhost:27017 --gzip --db daily_news ./daily_news
```

## npm Compile

```
npm run dev
```

## Start Server

Start the local development server

```
php artisan serve
```

You can now access the server at http://localhost:8000
