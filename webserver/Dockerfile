ARG USERNAME=docker
ARG USER_UID=1000
ARG USER_GID=$USER_UID

FROM php:8.0-apache

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y git unzip zip iputils-ping vim

WORKDIR /var/www/html

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions gd pdo_mysql bcmath zip intl opcache pgsql pdo_pgsql

COPY --from=composer:2.3.7 /usr/bin/composer /usr/local/bin/composer


# Create the user
RUN useradd -rm -d /home/docker -s /bin/bash -g root -G sudo -u 1001 docker

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME
