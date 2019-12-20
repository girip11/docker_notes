# Dockerfile basics

* Default docker file name is **Dockerfile**. Can provide docker file with different name using **-f** option when building the image.

* Each line is called a **stanza**
* Each stanza is a layer. Order is important.
* Each keyword is written in **uppercase**.

## Good practices

* To minimize layers, combine many shell statements using &&.

```Dockerfile
# The below stanzas creates two layers
RUN apt-get update
RUN apt-get install curl
```

The above snippet can be rewritten to produce a single layer.

```Dockerfile
RUN apt-get update \
    && apt-get install curl
```

* ![Docker 19.03: Dockerfile Reference](./DockerfileReference.png)

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)

* [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
