# Set up Docker Compose and Wordpress

## TLDR
Read these two links:
- https://docs.docker.com/compose/wordpress/
- https://github.com/docker-library/wordpress/issues/10#issuecomment-88389890

## Tutorial
https://docs.docker.com/compose/wordpress/

## Modifications
To get this working with any theme, you'll need to make these changes:

## PHP File Upload Size
To be able to import assets over 1MB (including Wordpress XML exports):

From: https://github.com/docker-library/wordpress/issues/10#issuecomment-88389890

### Create uploads.ini first

Copy uploads-template.ini to uploads.ini

file_uploads = On
memory_limit = 64M
upload_max_filesize = 64M
post_max_size = 64M
max_execution_time = 600

### Add uploads.ini to volumes:

```
…
wordpress:
  depends_on:
    - db
  image: wordpress:latest
  ports:
    - "8000:80"
  restart: always
  volumes:
    - ./wp-content:/var/www/html/wp-content:rw
    - ./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini:rw
  environment:
    WORDPRESS_DB_HOST: db:3306
    WORDPRESS_DB_USER: wordpress
    WORDPRESS_DB_PASSWORD: wordpress
…
```

### Volumes Explained
`- ./wp-content:/var/www/html/wp-content:rw`
map wp-content folder to a folder on the computer

`- ./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini:rw`
map your newly created uploads.ini with the actual file on your image

## Commands to Keep In Mind

### up
$ docker-compose up -d

### log into box
$ docker exec -it image_name /bin/bash
$ docker exec -it my_wordpress_wordpress_1 /bin/bash
