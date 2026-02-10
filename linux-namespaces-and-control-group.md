# Explore Linux Namespaces and Control Group (cgroup)

## Run multiple containers in shared namespaces
- You can share name spaces by running a container with a flag container the target containers ids such as pid, ipc, network namespaces
- e.g. `docker run -it --name sidecar \
  --pid container:target \
  --ipd container:target \
  --network container:target \
  alpine sh`
- while in this interactive shell mode, you can check details using `ps` `ps aux` `hostname` `ip addr` etc.

## Execute host commands in a container's namespace
- If an image is distroless (no shell, no package manager, no http clients), you cannot use `docker exec` on it
- you may need to use other methods to query it
- you can do this using nsenter and the --net and --target pid flags using the main containers PID
- e.g. `sudo nsenter --net --target 3266 curl http://127.0.0.1:15000`

## Limit container's CPU and memory (cgroup)
- Sometimes you may need to limit a hungry containers usage
- To check the stats of the containers you can use `docker stats` or `docker stats <container name>` - check your servers cpu and memory using `nproc` and `free -h`
- stop the container with high usage using `docker stop <container name>`
- remove it before starting a new one
- restart it with usage limits
- e.g. `docker run -d \
  --name hoggy \
  --cpus="0.5" \
  -m 500m \
  ghcr.io/iximiuz/labs/resource-hog/herder:v1.0.0`

  ## Freeze and thaw linux processes (cgroup)
  - - Freezing a process lets you safely pause it without stopping or killing it, useful when you need to suspend a heavy job during peak load or stopping the load so you can inspect the systems state during a bug investigation
  - - To run a process in its own cgroup, first find out which cgroup it is in
    - using `which <process name>` e.g. `which omnihog`
    - create a directory under /sys/fs/cgroup
    - e.g. sudo mkdir /sys/fs/cgroup/omnihog
    - 
