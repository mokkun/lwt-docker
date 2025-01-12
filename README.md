# Learning With Texts with Docker

LWT-docker sets up a container running an apache2 server with [learning with texts](https://learningwithtexts.com/).

This image is also available on DockerHub as [suzanje/lwt](https://hub.docker.com/r/suzanje/lwt).

## Usage

*if you cloned this repo don't forget to build the image before running it*

The recommended way to run this docker file is by using a `docker-compose.yml` file 

```yaml
version: '3'

services:
  mariadb:
    image: mariadb:10.6
    restart: always
    environment:
      - "MARIADB_USER=lwt"
      - "MARIADB_PASSWORD=qwerty"
    volumes:
      - media/:/var/lib/mysql
  lwt:
    image: lwt:latest
    restart: always
    environment:
      - "MARIADB_SERVER=mariadb"
      - "MARIADB_USER=lwt"
      - "MARIADB_PASSWORD=qwerty"
    ports:
      - "8080:80"
    depends_on:
      - mariadb
```

You can also probably run it with docker-run like the following

```shell
docker run -d --port "80:8080" --link mariadb_container -e MARIADB_SERVER=db -e MARIADB_USER=lwt -e MARIADB_PASSWORD=qwerty lwt
```

