# Docker hub

* Official images will have **official** tag on it and the name without a slash on it. In otherwords, official images will not have any **username or organization name**

* Dockerfile for official images can be found at [docker-library official-images](https://github.com/docker-library/official-images)

* A docker image can have multiple tags associated with it.

```bash
# latest nginx image
# same as `docker pull nginx`
# default tag is latest
docker pull nginx:latest

# mainline and latest are tags associated with latest docker image
# Image will be downloaded only once
docker pull nginx:mainline

# both image entries should have same image ID
docker image ls
```

* When considering non official repositories, **look for number of stars and pulls**.

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
