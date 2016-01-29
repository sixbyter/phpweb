# PHPWEB

A docker image for php development and it is very suitable for Laravel. i don't recommend to use it in production.


## Info

Detail is in [Dockerfile](https://github.com/sixbyter/phpweb/blob/master/image/Dockerfile).

what was it installed ?

- php 7.0.2
- composer
- laravel/envoy
- laravel/installer
- nodejs 5.5.0
- npm 3.3.12
- nginx 1.9.9
- gulp
- bower
- grunt-cli
- pm2
- supervisor
- cron
- git


## Require

please you have installed `docker` and `docker-composer` before use

## Usage

pull:

```
git clone git@github.com:sixbyter/phpenv-docker.git
```

cd dir:

```
cd phpweb
```

run `docker-composer`:

```
docker-composer up -d
```

also, you can build a new one:

```
git clone git@github.com:sixbyter/phpenv-docker.git
cd phpweb/image
docker build -t sixbyte/phpweb .
cd ..
docker-composer up -d
```


