# Laravel Docker With Formatter

## About

This is boilerplate for Laravel and Docker and also includes formatters.

## Setup

- To get started, make sure you have Docker installed on your system, and then clone this repository.
- Install or copy your laravel project to `src` directory.
- Default exposed ports are following. You can change in `docker-compose.yml` or `src/.env`
    - nginx - 80
    - mysql - 3306
    - redis - 6379
    - mail - 1000
- Build docker
```
docker-compose build
```
- Start docker
```
docker-compose up -d
```
- Or start by passing environment variable from laravel
```
docker-compose -d --env-file ./src/.env up
```
Three additional containers are included that handle Composer, NPM, and Artisan commands without having to have these platforms installed on your local computer. Use the following command examples from your project root, modifying them to fit your particular use case.

- `docker-compose run --rm composer install`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate`

## Compiling Assets

In order to get started, you first need to add `--host 0.0.0.0` after the end of your relevant dev command in `package.json`. So for example, with a Laravel project using Vite, you should see:

```json
"scripts": {
  "dev": "vite --host 0.0.0.0",
  "build": "vite build"
},
```

and then add `server` option in `vite.config.js` like this:

```js
export default defineConfig({
    plugins: [
        ...
    ],
    server: {
        hmr: {
            host: 'localhost',
        },
    },
});
```
- Then, run the following commands to install your dependencies and start the dev server:
```
docker-compose run --rm npm install
```
```
docker-compose run --rm --service-ports npm run dev
```
- Want to build for production? Simply run 
```
docker-compose run --rm npm run build
```

## Formatter

There are 3 formatter used to format html, blade, css, js, vue, react, php, laravel before git commit:
- bladeformatter
- pretter
- pint
  
First things first, you need to install above 3 package by following command:

```
docker-compose run --rm npm i blade-formatter prettier --save-dev
```
```
docker-compose run --rm composer require laravel/pint --dev
```

Then copy the formatter config files to `src` directory

```
cp formatter/.bladeformatterrc.json formatter/.prettierrc formatter/pint.json src
```

Copy `pre-commit` file to `.git` direcotory to format whenever commit in git

```
cp formatter/pre-commit .git/hooks/pre-commit
```

## Usage

App
```
http://localhost
```

PHP Myadmin
```
http://localhost:8080
```

Mail
```
http://localhost:1000
```

Note: Ports can be change depend on your config.
