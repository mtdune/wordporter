# WordPorter

![WordPorter](logo.png)
<!--- https://www.silhouette-illust.com/illust/40327 -->

## Introduction

WordPorter is Docker files for WordPress developer.
Clean development environment on official WordPress Docker image.

## Requires

- Docker for your operating system
  - Windows user is required professional license for Hyper-V

## Getting Started

### How to install

Clone this git repository to your computer.

```bash
git clone https://github.com/mtdune/wordporter.git
```

### How to run

```bash
docker-compose build
docker-compose up -d
```

View to <http://localhost:8000>

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

Debian GNU/Linux 9 from Official WordPress image.

- Apache 2.4.25 or later
  - netstat -uptap
  - apachectl -v
- PHP 7.2 or later
- rbenv 1.1.2 or later
- ruby 2.4.2 or later
- gem 2.6.13 or later
- Wordmove 4.0.0 or later
- WP-CLI 2.1.0 or later
