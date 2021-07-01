# Multi stage builds with Docker

> Unless you’re very careful, Docker’s build cache often won’t work for multi-stage builds—and that means your build is slow.

```Dockerfile
# This is the first image:
FROM ubuntu:18.04 AS compile-image
RUN apt-get update
RUN apt-get install -y --no-install-recommends gcc build-essential

WORKDIR /root
COPY hello.c .
RUN gcc -o helloworld hello.c

# This is the second and final image; it copies the compiled binary
# over but starts from the base ubuntu:18.04 image.
FROM ubuntu:18.04 AS runtime-image

COPY --from=compile-image /root/helloworld .
CMD ["./helloworld"]
```

> If you only have the final image in your Docker image cache when you do another build, your cache will be missing all of the earlier images(of the multi stage build), the images you require to do earlier stages of the build. And that means your caching is useless, you will need to rebuild everything from scratch, and your builds will be slow.

**SOLUTION**: If you want to have fast builds you need to ensure that the earlier stages—like the stage with the compiler—are also in the Docker image cache.

```Bash
#!/bin/bash
# build script
set -euo pipefail
# Pull the latest version of the image, in order to
# populate the build cache. This isn't necessary if
# you're using BuildKit.
docker pull itamarst/helloworld:compile-stage || true
docker pull itamarst/helloworld:latest        || true

# Build the compile stage:
docker build --target compile-image \
       --build-arg BUILDKIT_INLINE_CACHE=1 \
       --cache-from=itamarst/helloworld:compile-stage \
       --tag itamarst/helloworld:compile-stage .

# Build the runtime stage, using cached compile stage:
docker build --target runtime-image \
       --build-arg BUILDKIT_INLINE_CACHE=1 \
       --cache-from=itamarst/helloworld:compile-stage \
       --cache-from=itamarst/helloworld:latest \
       --tag itamarst/helloworld:latest .

# Push the new versions:
docker push itamarst/helloworld:compile-stage
docker push itamarst/helloworld:latest
```

---

## References

- [Multi stage builds](https://pythonspeed.com/articles/faster-multi-stage-builds/)
