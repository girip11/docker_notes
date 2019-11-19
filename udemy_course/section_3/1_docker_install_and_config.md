# Docker Install and Configuration

* Docker client and server(docker daemon) versions `docker version`. Docker client queries the docker daemon for these details. With this command we can verify the docker client server communication as well.

* `docker info` - system wide information and also informations on the docker engine.

* `docker --help`

* `docker <command>` . Example `docker run`. This is a old way of invoking. Still works.

* `docker <mgmt_command> <sub_command>` is a **new way of invoking commands**. To know more about a particular management command `docker <mgmt_cmd> --help`

~~~bash
docker --help

# container is a management command
docker container --help
~~~

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
