# Docker DNS

* Docker daemon has builtin dns server that containers use by default.

* Containers can reach each other using container name.

* Default bridge network doesnot have DNS facility and hence containers on default bridge network cannot reach each other by name. This can be overcome by using `--link` optino of `docker container run` command. But it is recommended to create a new network and use that network.

~~~bash
docker network ls

docker network create my_app_net

docker network ls

docker container run -p 80:80 -d --name nginx --network my_app_net nginx

# get in to alpine container
docker container run -it --name alpine --network my_app_net alpine

# ping the nginx container from the alpine container
ping -c 2 nginx
~~~

**NOTE**: Docker compose takes care of new virtual network for an app. So communication between various containers in the app can happen using DNS.

## DNS alias

* `docker container run --network-alias <domain_name>` or `docker container run --net-alias <domain_name>` - can make different containers respond to the same DNS domain name, given those containers are connected to the same bridge network.

* Verify with `nslookup <domain_name>`

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
