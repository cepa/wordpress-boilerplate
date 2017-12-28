# Wordpress Boilerplate

This repo contains a simple boilerplate for Wordpress development including:
- Vagrant environment
- Docker compose setup
- Basic MySQL installation
- Basic Wordpress installation
- Nginx configuration

## Build and run VM environment
You will need Vagrant to create the environment, additionally you need to install the hosts-updater plugin.
~~~
vagrant install plugin vagrant-hostsupdater
vagrant up
vagrant ssh
~~~

## Build and run Docker
~~~
docker compose build
docker compose up -d
docker compose logs -f
~~~

## Create database for Wordpress
~~~
echo "DROP DATABASE IF EXISTS wordpress" | docker exec -it mysql mysql -u root -p'secret'
echo "CREATE DATABASE wordpress" | docker exec -i mysql mysql -u root -p'secret'
echo "GRANT ALL PRIVILEGES on wordpress.* to wordpress@'%' IDENTIFIED BY 'wordpress'" | docker exec -i mysql mysql -u root -p'secret'
~~~

## Open Wordpress in a browser
Once the environment and Docker are built, simply go to: http://wordpress.dev to setup Wordpress.

## Where is my data?
The docker-compose.yml contains the following volumes to persist data:
- /srv/wordpress-boilerplate/mysql/data - MySQL database
- /srv/wordpress-boilerplate/wordpress/wp-content - Wordpress content, uploads, themes, etc
