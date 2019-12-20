# Running docker builds and extending official images

* Building images using the **build** command.

```bash
docker image build -t my_gtypist .
```

* Rebuilts all other layers from the layer that changes. Hence ordering of stanzas are very important.

* Things that change the least at kept at the top of the Dockerfile, while the things that change the most are placed at the bottom of the Dockerfile.

## Extending official images

* Using official alpine package as base image for building custom image.

```Dockerfile
FROM alpine:latest
```

* Extending base image of applications like nginx, mongo etc

```Dockerfile
FROM nginx:latest

WORKDIR /usr/share/nginx/html

COPY index.html .
```

## Cleanup unused images

```bash
# cleans up dangling images
docker image prune

# cleans up all unused images
docker image prune -a
```

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
