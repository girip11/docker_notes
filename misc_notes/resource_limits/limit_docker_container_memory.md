# Setting Memory And CPU Limits In Docker

There are multiple ways to limit a container's resource(CPU/memory) usage.

- Restricting while building the docker image. `docker image build --help`
- By associating the container with a **resource restricted cgroup**. `docker container run` accepts a **cgroup-parent** option as well.
- While launching the container using the **--memory** or `--cpus` option. `docker container run --help`. This will be container specific.

## Limit container cpu

```bash
docker container run --cpus=2 nginx

# cpu-shares acts like a priority of cpu allocation to the container
# higher cpu share means higher priority
docker container run --cpus=2 --cpu-shares=2000 nginx
```

## Limiting container memory

By default, a container can use all of its host's available memory.

```bash
# Take a note of the below commands output
docker info | grep -i memory

# launch a container with the below command and verify its
#  memory using docker container stats
docker container run --rm -it --name mem_no_limit alpine:latest sh

# In the "MEM USAGE / LIMIT" column, the limit should be the same as the
# docker info output
docker container stats mem_no_limit

# check memory stats
docker container inspect mem_no_limit | grep -i Memory
```

- From the container launched above, try the `free -m` command to check the available memory (should be a number close to the `docker info` command output).

### Memory limit using the run command's memory option

- Memory limit units k(KB), m(MB), g(GB) can be used.

```bash
# launch a container with the below command and verify its
#  memory using docker container stats
docker container run --rm -it --name mem_with_limit --memory 512m  alpine:latest sh

# In the "MEM USAGE / LIMIT" column, the limit should be the 512mb
docker container stats mem_with_limit
```

- `ContainerSwapMemory = (MemorySwap - Memory)`

- When the memory limit is set, **by default the container's swap memory value is twice the allowed memory value.** This means the container's allowed swap memory is same in size as its allowed memory.

```bash
# check the MemorySwap and memory columns
docker container inspect mem_with_limit | grep -i Memory
```

### Soft limit using `memory-reservation`

```bash
docker container run -m 512m --memory-reservation=256m nginx
```

### Swap

- To **disable swap**, set the **--memory** and **--memory-swap** options to the same value.

```bash
docker container run --rm -it --name mem_with_limit --memory 512m --memory-swap 512m alpine:latest sh

docker container stats mem_with_limit | grep -i Memory
```

**NOTE**: Memory option sets only the memory limit on the container. But inside the container, the memory is still same as the output of the `docker info` command. In the case where the container is launched with the memory option set, the container is killed when the memory usage exceeds the allowed value.

```bash
# observe the output of the below commands.
# Both see the available memory as same
docker container run --rm -it --name mem_no_limit alpine:latest free -m

docker container run --rm -it --name mem_with_limit --memory 512m --memory-swap 512m alpine:latest free -m
```

- To know if the container is killed because of **OutOfMemory(OOM)**, use the `docker container inspect` command.

```bash
# Limit the memory to 50MB and disable swap, and try to use 60MB
# Below command output look like
# stress: info: [1] dispatching hogs: 0 cpu, 0 io, 1 vm, 0 hdd
# stress: dbug: [1] using backoff sleep of 3000us
# stress: dbug: [1] setting timeout to 1s
# stress: dbug: [1] --> hogvm worker 1 [7] forked
# stress: dbug: [7] allocating 62914560 bytes ...
# stress: dbug: [7] touching bytes in strides of 4096 bytes ...
# stress: FAIL: [1] (416) <-- worker 7 got signal 9
# stress: WARN: [1] (418) now reaping child worker processes
# stress: FAIL: [1] (422) kill error: No such process
# stress: FAIL: [1] (452) failed run completed in 0s
docker container run --name memory_limit_stress --memory 50m --memory-swap 50m -it polinux/stress stress --vm 1 --vm-bytes 60M --timeout 10s


# prints "OOMKilled": true
docker container inspect memory_limit_stress | grep -i oom
```

- When memory limit is set while launching the container, the same reflects in the cgroup file **memory.limit_in_bytes**. Get the **docker container ID** and search for the same inside the **`/sys/fs/cgroup/memory`** directory, if the cgroup is not known (default cgroup is **docker**). We can also check the cgroup to which the container belongs to using `systemd-cgtop` if the container is using systemd cgroup

```bash
# This should print the memory limit set
cat /sys/fs/cgroup/memory/docker/<container_id>/memory.limit_in_bytes

# or in case of cgroup v2
cat /sys/fs/cgroup/docker/<container_id>/memory.max
```

---

## References

- [Understanding Docker Container Memory Limit Behavior](https://medium.com/faun/understanding-docker-container-memory-limit-behavior-41add155236c)
- [How to limit a docker container’s resources on ubuntu 18.04](https://hostadvice.com/how-to/how-to-limit-a-docker-containers-resources-on-ubuntu-18-04/)
- [How Docker uses cgroups to set resource limits?](https://shekhargulati.com/2019/01/03/how-docker-uses-cgroups-to-set-resource-limits/)
- [Setting Memory And CPU Limits In Docker](https://www.baeldung.com/ops/docker-memory-limit)
- [Docker Container CPU Limits Explained](https://www.thorsten-hans.com/docker-container-cpu-limits-explained/)
- [Docker Container Memory Limits Explained](https://www.thorsten-hans.com/limit-memory-for-docker-containers/)
- [Setting Memory And CPU Limits In Docker](https://www.baeldung.com/ops/docker-memory-limit)
