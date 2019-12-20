# Persistent data

* Volumes need manual deletion. To persist data out of containers.
* `VOLUME` stanza in Dockerfile defines a volume. Every time a container is lauched for that image, a new volume is created

```bash
# to know about the volume location
docker container inspect <container_name>

# list all the volumes
docker volume ls

# delete volume
docker volume prune -a
```

## Named volumes

* Using named volume, multiple containers can share the same volume.
* Same volume can be used when lauching a new container when the old container died.

```bash
# creates a volume with name mysql_volume
docker container run --rm -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD \
-v mysql_volume:/var/lib/mysql mysql:latest

docker container inspect mysql

docker volume ls
```

## Creating volume

```bash
docker volume create --help
```

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
