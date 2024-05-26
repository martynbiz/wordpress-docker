# Wordpress Docker 

This is a starter Docker container for Wordpress 

## Getting started 

Copy the docker-compose and uploads ini files:

```
$ cp docker-compose.yml-example docker-compose.yml
$ cp uploads.ini-example uploads.ini
```

Start the container (without passing env variables, might use defaults.. not tested this)

```
$ MYSQL_ROOT_PASSWORD=wordpress MYSQL_PASSWORD=wordpress docker-compose up -d
```

## Build specification

To extend the default images, there is the possiblity of adding a /build directory and putting Dockerfiles there:

e.g. 

/build/wordpress/Dockerfile

Then amend the docker-compose file (remove image attribute):

```
wordpress:
  build: ./build/wordpress
```

The build directory will be ignored by the repository (see .gitignore)

## Production 

This is some additional things to run Wordpress on production server

Environment variables

Change docker-compose passwords to environment variables and pass in with `docker-compose up`:

Update any docker-compose.yml environment variables with:

```
MYSQL_PASSWORD: ${MYSQL_PASSWORD}
```

Run `docker-compose up` (space at front won't commit command to history)

```
$  MYSQL_ROOT_PASSWORD=rootpw MYSQL_PASSWORD=pw docker-compose up -d
```

Docker image 

Would like to use `php8.3-fpm-alpine` instead of `php8.3-apache`, but container wouldn't start properly.


## Troubleshooting

Use this command to view environment variables within Docker 

```
docker inspect --format '{{json .Config.Env}}' <container_name_or_id>
```

Issues with sending emails

Wordpress does not send emials from docker containers without some modification to the docker build or via plugins. Currently looking into plugins such as WP Mail SMTP.


Undefined constant PDO::MYSQL_ATTR_INIT_COMMAND

Encountering this when using FG Joomla to WordPress plugin. 

```
$ docker-php-ext-install pdo pdo_mysql
```






nate access to shared updraft backup.. 
nate access to spsc-dev site ssh
deploy 
wp-cli 
limit blocks available to content editor 



natakallum
