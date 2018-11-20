Set up a local Wordpress Docker containers (mysql and php) using the official Docker Compose tutorial (https://docs.docker.com/compose/wordpress/).

The difference between using this repository and the official tutorial is that this `docker-compose.yml` sets up your `wp-contents` folder as a shared folder and creates a symlink to the php `uploads.ini` config file. Having access to the `uploads.ini` file allows you to set the upload limit for PHP, which by default is set to only 1MB. A complete `uploads.ini` is included in this repository.

## Simple Setup

1. Install and start Docker.
2. Clone this project `git clone git@bitbucket.org:keeeeeegan/docker-wordpress.git`.
3. cd into directory: `cd docker-wordpress`
4. Run the command to start the docker containers: `docker-compose up -d`.
5. Go to http://localhost:8000.

## Handy Docker Compose Commands

Docker Compose Commands to keep In mind, to make your life easier.

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
