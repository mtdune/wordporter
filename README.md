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
mkdir ./my-local-directory
cd ./my-local-directory
git clone https://github.com/mtdune/wordporter.git
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

- Password not required.

```bash
docker exec -it wp /bin/bash
```

### When finished

```bash
docker-compose down -v
```

## Environments

Debian GNU/Linux 9 from official WordPress image.

- Apache 2.4.25 or later
- PHP 7.2 or later

WordPress

- Wordmove 4.0.0 or later
- WordPress 5.1 or later
- WP-CLI 2.1.0 or later

ruby

- rbenv 1.1.2 or later
- ruby 2.4.2 or later
- gem 2.6.13 or later
