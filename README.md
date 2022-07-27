# Install Netdata with Docker

You can use Docker Compose to easily run WordPress in an isolated environment built with Docker containers. This quick-start guide demonstrates how to use Compose to set up and run WordPress. Before starting, make sure you have Compose installed.

# Define the project


1.Create an empty project directory. \

You can name the directory something easy for you to remember. This directory is the context for your application image. The directory should only contain resources to build that image. \

This project directory contains a docker-compose.yml file which is complete in itself for a good starter wordpress project. \
```bash

    Tip: You can use either a .yml or .yaml extension for this file. They both work.
```
2.Change into your project directory.

For example, if you named your directory my_wordpress:
```bash

 cd my_wordpress/

```
3.Create a docker-compose.yml file that starts your WordPress blog and a separate MySQL instance with volume mounts for data persistence:

```yml
services:
  db:
    image: mariadb:10.6.4-focal
    command: '--default-authentication-plugin=mysql_native_password'
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    expose:
      - 3306
      - 33060
  wordpress:
    image: wordpress:latest
    ports:
      - 80:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
```
# Build the project 
Now, run docker compose up -d from your project directory. \

This runs docker compose up in detached mode, pulls the needed Docker images, and starts the wordpress and database containers, as shown in the example below.
