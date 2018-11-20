# Set up Docker Compose and Wordpress

Based on:
* https://docs.docker.com/compose/wordpress/

## Mods
We'll want to make the following changes to the `docker-compose.yml` file we get after the tutorial:

Set port to 8000 instead of 80:
```
…
ports:
  - "8000:80"
…
```

Add a `wp-content` folder to the `wordpress` volume so we can actually edit files:
```
…
volumes:
  - ./wp-content:/var/www/html/wp-content:rw
…
```

## PHP File Upload Size
To be able to import assets over 1 MB (e.g. Wordpress XML exports):

(From: https://github.com/docker-library/wordpress/issues/10#issuecomment-88389890)

### Ensure you have an uploads.ini first

Open `uploads.ini`, or create a new `uploads.ini` and make sure it looks like the following:
```
file_uploads = On
memory_limit = 64M
upload_max_filesize = 64M
post_max_size = 64M
max_execution_time = 600
```
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

Map wp-content folder to a folder on the computer.

`- ./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini:rw`

Map your newly created uploads.ini with the actual file on your container.

## Commands to Keep In Mind

### Compose up
`$ docker-compose up -d`

### Compose down
`$ docker-compose down`

### Log into box
`$ docker exec -it {container name} /bin/bash`

After following the tutorial, our container name should be `my_wordpress_wordpress_1`:

`$ docker exec -it my_wordpress_wordpress_1 /bin/bash`

### List containers (if you don't know the container name)
`$ docker container ls`
