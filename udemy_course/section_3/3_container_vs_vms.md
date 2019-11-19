# Container and VM

* Containers are just restricted processes inside host OS.

~~~bash
# start a nginx container
docker container run --publish 80:80 --detach --name webserver nginx

# verify the container is up and running
docker container ls

# process inside a container
docker top webserver

# ps on the host works
# results processes with same PID on the host as well.
pgrep -af nginx
~~~

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
