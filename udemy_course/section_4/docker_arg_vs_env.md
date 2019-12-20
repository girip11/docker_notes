# `ARG` vs `ENV`

> ENV is for future running containers. ARG for building your Docker image.

* Dockerized applications can access the environment variables. Hence suitable for passing configuration to the application as `ENV` variables.

**NOTE**: ARG values are not available after the image is built. A running container won’t have access to an ARG variable value.

* Both ARG and ENV are available during **docker image build phase**.

```Dockerfile
ARG port=3000

ENV USER=postgres

RUN echo $port
RUN echo $USER
```

* To change/set default value `ENV` during image building, `ARG` can be used.

```Dockerfile
# Can be assigned a value using `--build-args` while building the image.
ARG version

# can be changed during the `docker container run` command using the '-e' or '--env' option
ENV DB_VERSION=${version:-1.0.0}
```

---

## References

* [Docker `ARG` vs `ENV`](https://vsupalov.com/docker-arg-vs-env/)
