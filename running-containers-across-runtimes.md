# Beyond Docker: Run Containers Across Runtimes

## Start and inspect containers with Podman
- Podman is an alternative to docker that aims to be more secure, daemonless, and rootless 
- To run a container with podman, use `podman run` instead of `docker run` followed by any other options just like with docker run
- Other commands function similary as well, such as `podman ps` will show you the running containers
- if you run a container using sudo or without sudo, they will be different container environments, this means when using docker or podman inspect, ps, you will have to use the sudo command or you will be looking at a different container
