# WordPress Docker

A starter Docker Compose setup for running WordPress with a MariaDB database.

It runs two containers:

- `wordpress` – WordPress 7.1 on PHP 8.3 with Apache, served on port 8000 by default (set `WORDPRESS_PORT` to change it)
- `db` – MariaDB 10.6, with data stored in the `db_data` Docker volume

Themes, plugins and uploads live in `./wp-content` on the host, so they can be edited directly and survive container rebuilds. PHP upload limits are set in `uploads.ini`.

Database credentials are read from a `.env` file. Any variable that is not set falls back to the default of `wordpress` (the database host defaults to `db:3306`).

## Getting started

### Development

1. Copy the PHP uploads config and the environment file:

   ```
   $ cp uploads.ini-example uploads.ini
   $ cp env.example .env
   ```

   The values in `env.example` match the defaults, so `.env` works for local development without changes.

2. Start the containers:

   ```
   $ docker compose up -d
   ```

3. Open http://localhost:8000 and follow the WordPress installer.

To stop the containers:

```
$ docker compose down
```

### Production

Do not use the default credentials on a server.

1. Copy the PHP uploads config and adjust the limits if needed:

   ```
   $ cp uploads.ini-example uploads.ini
   ```

2. Create a `.env` file from the example:

   ```
   $ cp env.example .env
   ```

   Then edit `.env` and replace every password with a strong, unique value. Do not keep the `wordpress` defaults.

   `MYSQL_USER`/`MYSQL_PASSWORD` and `WORDPRESS_DB_USER`/`WORDPRESS_DB_PASSWORD` must match. `.env` is ignored by git, so it will not be committed. Restrict who can read it:

   ```
   $ chmod 600 .env
   ```

3. Start the containers:

   ```
   $ docker compose up -d
   ```

4. Check that the containers are using the expected values:

   ```
   $ docker compose config
   ```

The database credentials only take effect when the `db_data` volume is first created. To change them later, change them in MariaDB itself, or back up the site and recreate the volume.

WordPress is served over plain HTTP on `WORDPRESS_PORT` (8000 by default). For HTTPS, put a reverse proxy (e.g. Nginx, Caddy or Traefik) in front of it.
