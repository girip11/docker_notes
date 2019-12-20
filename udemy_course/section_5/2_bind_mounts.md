# Bind mounts

* Mapping host files to container files. Very helpful in development environment. Hosts and container can share the code.

```bash
# creates a volume with name mysql_volume
docker container run --rm -d -p 8080:80--name myapp \
-v $(pwd)/src:/usr/share/src myapp:latest
```

---

## References

* [Udemy docker course by Bret Fisher](https://www.udemy.com/share/101WekCUMfd1lVR34=/)
