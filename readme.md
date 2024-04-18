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


The following process was used to change the database to a different environment/version:

1) Take a backup of the website database using Updraft

2) Stop and remove the existing database container only

```
$ docker stop <container_name>
$ docker rm <container_name>
$ docker volume rm <volume_name>
```

3) Update the version in the docker-compose.yml file:

```
services:
  db:
    image: mariadb:10.6.17
    ...
```

4) Run the container to create the new database container:

```
$ docker-compose up -d
```

5) Restore the backup