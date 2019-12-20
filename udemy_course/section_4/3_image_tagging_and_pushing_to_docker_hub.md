# Image Tagging

* Official images will not have any **username or organization name**

* Docker hub repository name format- **<username/organization>/reponame**
Ex: mysql/mysql-server

```bash
docker pull mysql/mysql-server:latest
```

* We can have private and public repos in docker hub.

```bash
# with this command we can assign tags to existing images
docker image tag --help

# username/reponame required format for pushing images to dockerhub
docker image tag nginx:latest girip/nginx

# used for logging in to dockerhub
docker login

# push the image to dockerhub
docker image push girip/nginx

# to logout of the account
docker logout
```

* While uploading and downloading images, only new layers are pushed or pulled.

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
