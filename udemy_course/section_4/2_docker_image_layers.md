# Docker image layers

* Union file system
* To list the layers on docker image use **history** command

```bash
docker image history nginx:latest
```

* Images are a stack of layers.
* Observe that every statement in the **Dockerfile** becomes an image layer.
* Every layer has its own SHA hash.
* **Not every layer will occupy disk space**. For instance, `ENV` statement just contributes to metadata change and hence its size value is 0bytes.

* Containers are another read/write layer on top of the base image. Multiple container instances of the same base image will share the image layers.

* Docker image layers are mounted as read only. If any file present in the image is changed from within the container, a copy of that file is stored in that read/write layer of that container. This is referred to as **copy on write**. Other containers using the same image will remain unaffected.

* Only the final image layer is assigned an **image ID**.

```bash
# Observe the <missing> on image layers
docker image history nginx:latest

# inspecting an image
# This will list the RootFS layers, ENV, volumes etc
docker image inspect nginx:latest
```

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
