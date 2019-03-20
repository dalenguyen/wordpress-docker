# WordPress Docker Workflow

This is how you set up local WordPress development with Docker

## Getting started

Clone this project

```sh
git clone https://github.com/dalenguyen/wordpress-docker.git
```

## Generate an image of docker-compose.yml

```sh
docker run --rm -it --name dcv -v $(pwd):/input pmsipilot/docker-compose-viz render -m image docker-compose.yml
```

## Start the containers

```sh
docker-compose up -d
docker-compose ps
```

## Create wp-config.php

After bring the machines up, we create wp-config.php before installing

```sh
docker-compose run wp core config --dbname=wordpress --dbuser=wordpress --dbpass=wordpress --dbhost=mysql --dbprefix=wp_
```

## Configure WP site

```sh
docker-compose run wp core install --url="http://localhost:8080" --title="Docker WordPress" --admin_user="admin" --admin_password="password" --admin_email="email@example.com"
```

## Installing plugins

```sh
docker-compose run wp plugin install jetpack --activate
docker-compose run wp theme install customizr --activate
```

## Export database to wordpress/export folder

```sh
docker-compose run wp db export --add-drop-table /export/wordpress.sql
docker-compose run wp db import /export/wordpress.sql
```

## Reference

[Mastering Docker](https://www.packtpub.com/virtualization-and-cloud/mastering-docker-second-edition)