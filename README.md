Base PHP with Apache Docker Container
=====================================

### Fork by karfau

Simplifing images so they work for me when  developing a page using [Grav](https://getgrav.org/) in branches ending with `-grav-dev`.

Example `docker-compose.yml` inside the grav folder:
```yaml
version: '2'

services:
  php:
    build: path/to/local/clone/docker-php-apache-base
    volumes:
          - .:/var/www/html
    ports:
      - "80:80"
```

- avoid using composer inside the docker image, or all (updated?) files will be owned by root


### Original README continues

Dockerized environment for PHP web development and Apache web server.

Features
--------

* Ability to set Apache document root through `APACHE_DOC_ROOT` environment variable. Default document root is `/var/www/html`
* Ability to set an Alias through `APACHE_DOC_ROOT_ALIAS` (no trailing slash!)
* Enabled Apache modules: rewrite
* Ability to set PHP `date.timezone` through `PHP_TIMEZONE` environment variable. Default timezone is `Europe/Rome`
* Enabled PHP extensions: gd, mcrypt, intl, mysql, mysqli, pdo_mysql, mbstring, soap, opcache, zip, xls
* Composer installed globally at `/usr/local/bin/composer`
* Xdebug PHP extension installed but not enabled
* Ability to enable xdebug PHP extension through `XDEBUG_ENABLE` environment variable which has to be set to `1`
* Ability to enable [memprof](https://github.com/arnaud-lb/php-memory-profiler) PHP extension through `MEMPROF_ENABLE` environment variable which has to be set to `1`
* Ability to set xdebug.remote_enable setting through `HOST_IP` environment variable.
* GIT installed (required by Composer)
* sSMTP installed (as Mail Transfer Agent for PHP mail function)
* Ability to set sSMTP mailhub, AuthUser and AuthPass through `SSMTP_MAILHUB`, `SSMTP_AUTH_USER` and `SSMTP_AUTH_PASS` environment variables
* MySQL CLI Client, vim installed

Usage
-----

Standalone usage example with host's current working directory as document root:

	$ docker run -p 80:80 -v $(pwd):/var/www/html webgriffe/php-apache-base

Credits
-------

[Webgriffe®](http://www.webgriffe.com/)



How to profile your page:
-------------------------

Before starting the docker container:
Set config variable XDEBUG_ENABLE to 1

Enable profiling by adding XDEBUG_PROFILE to the GET/POST Variables or as a cookie.

