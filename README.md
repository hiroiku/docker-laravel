# Docker Laravel

## Features

- One process one container
- MySQL ready
- PHP session using memcached
- Enabled Laravel Queue
- Enabled Laravel Task Scheduling
- Alternative Artisan commands that can be injected into PHP container

## Setup

Install Laravel

```sh
composer create-project --prefer-dist laravel/laravel laravel
```

## Start Docker Containers

```sh
docker-compose up
```

## Remove Docker Containers

```sh
docker-compose down
```

## Alternative Artisan Command

```sh
cd ./laravel/
composer artisan COMMAND
```

With options

```sh
cd ./laravel/
composer artisan COMMAND -- --OPTION_NAME OPTION_VALUE
```
