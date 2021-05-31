# laradock multi projects 🚀🐳

![badge1](https://img.shields.io/badge/laradock-12.1-yellow)
![badge2](https://img.shields.io/badge/laravel-8-brightgreen)
![badge4](https://img.shields.io/badge/docker-20.10-blue)

## create `test_laravel` project
- `composer create-project laravel/laravel test_laravel --prefer-dist`

## project structure
```sh
└laradock
└test_laravel
└project-2
```

## 1)project `laradock`
- copy from `default.conf` to `test_laravel.conf`
- add `127.0.01  test_laravel.test` in `sudo vim /etc/hosts`
- copy from `.env.example` to `.env`
- in `.env`:

### 1.1)db
```shell
MYSQL_DATABASE=default
MYSQL_PORT=3306
MYSQL_ROOT_PASSWORD=root
MYSQL_ENTRYPOINT_INITDB=./mysql/docker-entrypoint-initdb.d // Ex: laradock/mysql/docker-entrypoint-initdb.d/createdb.sql.example
```
### 1.2)project path
- `APP_CODE_PATH_HOST=../`
>in case just only 1 project:
>- `APP_CODE_PATH_HOST=../test_laravel/`

### 1.3)php
- `PHP_VERSION=7.4`

## 2)project `test_laravel`
- copy from `.env.example` to `.env`
- in `.env`:

### 2.1)db
```shell
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=default
DB_USERNAME=root
DB_PASSWORD=root
```

## deploy
1. `laradock# docker-compose up -d nginx mysql phpmyadmin redis workspace`
2. access on browser `test_laravel.test/public/index.php`
![demo](screenshot/demo.png)
3. `laradock# docker-compose exec (--user=laradock) workspace bash`
4. `cd test_laravel`
5. `/var/www/test_laravel# php artisan migrate`
access on browser `test_laravel.test:8081` > login with these info:
```shell
MYSQL_HOST=mysql
MYSQL_USERNAME=root
MYSQL_PASSWORD=root
```
![phpmyadmin](screenshot/phpmyadmin.png)
*****************
![db](screenshot/db.png)
