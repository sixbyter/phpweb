# phpenv-docker

This is a image about php development environment with docker

# Info

- php 7.0.2
- composer
- laravel/envoy
- laravel/installer
- nodejs 5.5.0
- npm 3.3.12
- nginx 1.9.9
- supervisor
- cron
- git


This env is not recommend for production


# Usage

please install `docker` and `docker-composer` before use

`git clone git@github.com:sixbyter/phpenv-docker.git`

`cd phpenv-docker/image`

`docker build -t sixbyte/homestead`

configurate `docker-composer.yml` file

`docker-composer up -d`

