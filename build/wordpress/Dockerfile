FROM wordpress:6.5.0-php8.3-apache

RUN \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    libicu-dev \
    libldap2-dev \
    ssmtp && \
    docker-php-ext-install intl && \
    docker-php-ext-enable intl && \
    docker-php-ext-install shmop && \
    docker-php-ext-enable shmop

# # modify ssmtp settings
# RUN sed -ri -e 's/^(mailhub=).*/\1smtp-server/' \
#     -e 's/^#(FromLineOverride)/\1/' /etc/ssmtp/ssmtp.conf

RUN \
    pecl install apcu && \
    docker-php-ext-enable apcu