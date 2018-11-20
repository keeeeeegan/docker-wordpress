# Set up Docker Compose and Wordpress

1. Clone this project
2. Run the command to start the docker containers: `docker-compose up -d`
3. Go to localhost:8000

# Docker Compose Commands to Keep In Mind

## Compose up
`$ docker-compose up -d`

## Compose down
`$ docker-compose down`

## Log into box
`$ docker exec -it {container name} /bin/bash`

After following the tutorial, our container name should be `my_wordpress_wordpress_1`:

`$ docker exec -it my_wordpress_wordpress_1 /bin/bash`

## List containers (if you don't know the container name)
`$ docker container ls`
