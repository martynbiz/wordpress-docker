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
