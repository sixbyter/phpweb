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

修改 `/etc/hosts` 文件:

```
127.0.0.1   phpweb.local
```

浏览器打开地址:

```
http://phpweb.local/
```


如果你要添加一个新的项目:

```
# 修改 docker-compose.yml 文件, 添加如下:
anotherphpweb:
    image: 'sixbyte/anotherphpweb'
    links:
      - "mysql-base:mysqldocker"
      - "redis-base:redisdocker"
    volumes:
      - /path/to/www:/var/www:rw
      - /path/to/anotherphpweb.conf:/etc/nginx/conf.d/anotherphpweb.conf
    environment:
      - VIRTUAL_HOST=anotherphpweb.local
    container_name: anotherphpweb
```
一个独立的容器可以保证运行环境的隔离.

如果你要定制配置:

```
volumes:
      - /path/to/www:/var/www:rw
      - /path/to/anotherphpweb.conf:/etc/nginx/conf.d/anotherphpweb.conf
      - /path/to/crontab.file:/root/crontab.file # crontab
      - /path/to/php-fpm.conf:/usr/local/etc/php-fpm.conf # php-fpm.conf
      - /path/to/php.ini:/usr/local/etc/php/php.ini # php.ini
```

可以通过 `volumes` 参数链接容器的任何文件, 实现动态修改.

## 项目的简便部署:

`docker` 的一个很好的理念, 开发-测试-生产, 运输 "集装箱". 确保环境的一致. 项目的版本更新和回滚也是非常的方便.

创建项目的镜像 `Dockerfile`:
```
FROM sixbyte/phpweb

RUN git clone xxxxxxxxxxx

RUN cp xxxxxxx /etc/nginx/conf.d/phpweb.conf

```

构建镜像:

```
docker build -t hello/world:0.1 .
```

提交镜像到测试仓库:

```
docker push hello/world:0.1
```

测试工程师进行测试, 无误后部署到生产环境:

```
docker pull hello/world:0.1
docker run -d hello/world:0.1
```


## 其他

这里对一些内容进行说明.

### 图解

![结构](https://raw.githubusercontent.com/sixbyter/phpweb/master/doc/F035DBB5-CE77-4C0C-8829-542A6C4F9AEE.png)

### 关于使用 `nginx-proxy`

github 地址: [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy)

本镜像可以不使用 `nginx-proxy`, 我使用的原因是希望每次访问 `web` 站点都是 `80` 端口. 能占用宿主 `80` 端口的只有一个容器, 当创建多个 `phpweb` 容器的时候就要使用其他端口, 所以比较好的方法是使用 `nginx-proxy` 做代理, 同时还解决了容器动态 `ip` 的配置问题, 稍作配置, 还能当负载均衡. 详细参考 [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy).

### 关于服务独立, `php-fpm` 是独立的一个容器

这个我试过, 其实很不好用, `fpm` 不适合用于处理静态文件, 而且项目的迁移, 部署都很不方便. 静态文件一般都是交给 `nginx` 这类 `web server` 处理的, 如果项目的静态文件都是在云端或者 `php` 也负责处理静态文件, 可以这样使用, 这个可以参考我的另一个项目dnrmp.
