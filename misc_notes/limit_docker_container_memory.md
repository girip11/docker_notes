# Limiting docker container memory

## Enabling swap

* `docker info` - If the output of this command contains **WARNING: Noswaplimitsupport**, then do the following as root user (below steps are applicable for ubuntu)
  * Add `GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"` to **/etc/default/grub**. Save the file
  * Execute the command `update-grub`
  * Reboot the system
* Verify if the warning has disappeared after reboot with `docker info` (no need to execute as root)

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

* From the container launched above, try the `free -m` command to check the available memory (should be a number close to the `docker info` command output).

There are multiple ways to limit a container's memory usage.

* Restricting memory while building the docker image. `docker image build --help`
* While launching the container using the **--memory** option. `docker container run --help`
* By associating the container with a **memory limit set cgroup**. `docker container run` accepts a **cgroup** option as well.

## Memory limit using the run command's memory option

* Memory limit units k(KB), m(MB), g(GB) can be used.

```bash
# launch a container with the below command and verify its
#  memory using docker container stats
docker container run --rm -it --name mem_with_limit --memory 512m  alpine:latest sh

# In the "MEM USAGE / LIMIT" column, the limit should be the 512mb
docker container stats mem_with_limit
```

* `ContainerSwapMemory = (MemorySwap - Memory)`

* When the memory limit is set, **by default the container's swap memory value is twice the allowed memory value.** This means the container's allowed swap memory is same in size as its allowed memory.

```bash
# check the MemorySwap and memory columns
docker container inspect mem_with_limit | grep -i Memory
```

* To **disable swap**, set the **--memory** and **--memory-swap** options to the same value.

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

* To know if the container is killed because of **OutOfMemory(OOM)**, use the `docker container inspect` command.

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
docker container run --name memory_limit_stress --memory 50m --memory-swap 50m -it progrium/stress --vm 1 --vm-bytes 62914560 --timeout 1s


# prints "OOMKilled": true
docker container inspect memory_limit_stress | grep -i oom
```

* When memory limit is set while launching the container, the same reflects in the cgroup file **memory.limit_in_bytes**. Get the **docker container ID** and search for the same inside the **`/sys/fs/cgroup/memory`** directory, if the cgroup is not known (default cgroup is **docker**).

```bash
# This should print the memory limit set
cat /sys/fs/cgroup/memory/docker/<container_id>/memory.limit_in_bytes
```

---

## References

* [Understanding Docker Container Memory Limit Behavior](https://medium.com/faun/understanding-docker-container-memory-limit-behavior-41add155236c)

* [How to limit a docker container’s resources on ubuntu 18.04](https://hostadvice.com/how-to/how-to-limit-a-docker-containers-resources-on-ubuntu-18-04/)

* [How Docker uses cgroups to set resource limits?](https://shekhargulati.com/2019/01/03/how-docker-uses-cgroups-to-set-resource-limits/)
