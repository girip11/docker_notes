# Docker compose

## Docker compose configuration YAML

* `services`, `volulmes` and `networks` sections in compose YAML.

* compose YAML format can be found at [Compose file reference](https://docs.docker.com/compose/compose-file)

```YAML
version: "3.7"

services:
  mywebapp:
    image: girip11/docker_image
    volumes:
      - .:/usr/share/src
    environment:
      ENV_VAR: VALUE

networks:

volumes:

```

## Docker compose CLI

* `docker-compose` is the CLI used for local development and testing. Not recommended to be used in production environment.

```Bash
docker-compose --help

# setup volumes,networks and starts all the containers based on the .yml
docker-compose up

# to run the containers in the background
docker-compose up -d

# to view the logs when containers are running in background
docker-compose logs

# list running containers
docker-compose ps

# list processes inside the containers
docker-compose top

# removes all the containers and deletes the volumes and networks created
docker-compose down

# remove named and anonymous volumes as well
docker-compose down -v

# --rmi option useful to remove images built and named by compose
# no image tag should be mentioned against the image built
docker-compose down --rmi local
```

* By default creates a private network using default driver.

## Build images using compose

* `docker-compose up` will build the image only when the image is not found in the image cache.
* `docker-compose build` or `docker-compose up --build` can be used for **rebuilding** images after modifications.

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
