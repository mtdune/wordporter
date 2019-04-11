# WordPorter

![WordPorter](logo.png)
<!--- https://www.silhouette-illust.com/illust/40327 -->

## Introduction

WordPorter is Docker files for WordPress developer.

### Features

- Clean development environment on [official WordPress Docker image](https://hub.docker.com/_/wordpress)
- You can use WordPress, [Wordmove](https://github.com/welaika/wordmove) and [WP-CLI](https://wp-cli.org/)
- Sharing local files and directories

### Requires

- Docker for your operating system
  - Windows user is required professional license for Hyper-V

### Support

I might answer a question at twitter.

- <https://twitter.com/mtdune>

## Getting Started

### How to install

Clone this git repository to your computer.

```bash
mkdir my-local-directory
cd my-local-directory
git clone https://github.com/mtdune/wordporter.git

# Copy your private key(OpenSSH format) to shared directory for Wordmove.
# Private key be will copy from ~/ssh to ~/.ssh directory.
cp ~/.ssh/id_rsa ./ssh/id_rsa
```

### How to run

```bash
docker-compose build
docker-compose up -d
```

After a few minutes. View to <http://localhost:8000>

### Shared local files and directories

- WordPress files to my-local-directory/wordpress/
- MySQL files to my-local-directory/mysql/

### SSH to WordPress Docker container

Root login to WordPress Docker container.

- Password not required

```bash
docker exec -it wp /bin/bash
```

### When finished

```bash
docker-compose down -v
```

## Wordmove

### Usage

```bash
# SSH to WordPress Docker container
docker exec -it wp /bin/bash

# Add to the list of known hosts for Wordmove
ssh -o StrictHostKeyChecking=no YOUR-SERVER-ADDRESS -l YOUR-SSH-USERNAME
# Enter exit command in YOUR-SERVER-ADDRESS

wordmove init
wordmove doctor # You all have to be successful. Please check below.
```

movefile.yml file is in my-local-directory/wordpress/movefile.yml directory. You can edit it in local by your favorite editor.

- movefile.yml is written in character code UTF-8 and newline code LF

```yaml:movefile.yml
global:
  sql_adapter: wpcli # You can choose default or wpcli
local:
  vhost: http://localhost:8000
  wordpress_path: /var/www/html # use an absolute path here
  database:
    name: "wordpress"
    user: "root"
    password: "wordpress" # could be blank, so always use quotes around
    host: "db" # "db:3306" isn't work.
    port: "3306"
production:
...
```

- sql_adapter: wpcli is DB adapter by WP-CLI search-replace command
- sql_adapter: default is Wordmove DB adapter in ruby language

See also [Wordmove](https://github.com/welaika/wordmove).

After edited movefile.yml file, execute wordmove pull command.

```bash
wordmove pull --all

wp search-replace 'https://YOUR-SERVER-URL' 'http://localhost:8000' --dry-run
wp search-replace 'https://YOUR-SERVER-URL' 'http://localhost:8000'
```

If you can't open <http://localhost:8000>, Use WordPress debug mode.

- wordpress/wp-config.php

```php
define( 'WP_DEBUG', false ); # true is enable WordPress debug mode.
```

### utf8mb4 Error under MySQL 5.1

If you can't PUSH to remote server by Wordmove, You have to manually import from MySQL dump file.

```bash
ssh YOUR-SSH-USERNAME@YOUR-SSH-SERVER
su -
mysql -uYOUR-MYSQL-USERNAME -p YOUR-DATABASE-NAME < wp-content/dump.sql
```

Notes

- WordPress 4.2 or later required utf8mb4 character code for wp-emoji support
- MySQL 5.5 or later can use utf8mb4 code
- Official MySQL Docker image version is MySQL 5.5 or later

## Installed environments

These softwares are automatic installation by Docker files.

- Debian GNU/Linux 9 from official WordPress image.
- Apache 2.4.25 or later
  - user name and user group are www-data:www-data
- PHP 7.2 or later

WordPress

- WordPress 5.1 or later
- Wordmove 4.0.0 or later
  - rbenv 1.1.2 or later
  - ruby 2.4.2 or later
  - gem 2.6.13 or later
  - WP-CLI 2.1.0 or later

## Wordmove Official Dockerfile

- <https://hub.docker.com/r/welaika/wordmove/>
