# PHPWEB

一个 `php` 开发专用的 `docker` 镜像, 这个环境非常适合 `Laravel` 框架开发. 本镜像目前没有在生产环境上尝试使用, 不建议在生产环境下使用.


## 内容

详细信息可以到查看 [Dockerfile](https://github.com/sixbyter/phpweb/blob/master/image/Dockerfile).

安装了以下内容:

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


## 依赖

使用本项目前, 请确保已经安装 `docker` 和 `docker-composer`

## 用法

拉取代码:

```
git clone git@github.com:sixbyter/phpenv-docker.git
```

切换目录:

```
cd phpweb
```

运行 `docker-composer` 命令:

```
docker-composer up -d
```


你也可以重新 `build` 一个镜像的方式运行:

```
git clone git@github.com:sixbyter/phpenv-docker.git
cd phpweb/image
docker build -t sixbyte/phpweb .
cd ..
docker-composer up -d
```


