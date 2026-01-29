# Execute commands in a running container

- Real world scenarios requring looking into running containers to debug issues
- `docker exec` executes command on a running container
- e.g. `docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`
- e.g `docker exec -it <container-name-or-id> <shell-executable>`
- e.g `docker exec -it app-1 sh` will open a shell in the running app-1 container
- to query in a shell container you can use curl or wget
- docker exec allows you to jump into running containers to troubleshoot issues
- instead of having to set up ssh, you can look into live containers and see what is going on
- docker exec + curl/wget is like having a "secret backdoor" into your containers for debugging. You can inspect, test, and diagnose without stopping or restarting anything.

## List containers and identify tasks
- you can use `docker ps` to list all running containers
- this will only show running containers, to see all containers including exited and crashed ones, use `docker ps --all`
- `--help` is always at your disposal if you can't think of what command to run to see something
- e.g. `docker ps --no-trunc` will show you the full container id and other details
- To see full details of a specific container use `docker inspect CONTAINER_ID|NAME` or more explicit version `docker container inspect CONTAINER_ID|NAME`

## Stop and restart containers
- use `docker ps` to see what containers are running
- remember to use `docker exec` to execute a command in a running container
- you can run commands directly without going into interactive mode e.g `docker exec 391741f8a243 cat /var/lib/app/ledger.txt`
- use the `docker stop <container id or name>` command to stop a running container
- use `docker container rm <container id or name>` to remove a container, make sure it is stopped first

## Restart containers on failure automatically
- you can change the restart policy of a container:
- `no`: The container will not restart after exiting (default).
- `unless-stopped`: The container will always restart on exit (even if the exit code is 0) unless it was explicitly stopped by the docker stop command.
- `always`: Almost the same as unless-stopped, but a stopped (by the docker stop command) container will also restart if the Docker daemon itself restarts.
- `on-failure`: The container will restart only when the process exits with a non-zero status
- Several docker commands allow setting the restart policy for a container:
- `docker create` - creates a new container with the specified restart policy.
- `docker update` - updates the restart policy for an existing container.
- `docker run` - creates and starts a new container with the specified restart policy.
- e.g. `docker update --restart on-failure app-1`

## Signal containerized applications
- there are commands inside commands, you can view them using `docker container <command> --help`
- use the `-s` flag to send signal to container
- e.g. `docker kill -s SIGUSR1 app-1`
- to check logs of a container use `docker container logs <container-name>`

## Pause and unpause running containers
- You may need to pause a container during peak hours to allocate resources, or when troubleshooting
- To run a container in the background, use the -d flag
- e.g. `docker run -d <container>`
- Running a container without this flag, puts you in attached mode which allows you to see all the outputs
- the `--name` flag allows you to give a name to the container identifier or url, allowing you to call it easier
- use `docker pause <container>` to pause a container
- use `docker unpause <container>` to unpause a container
- use `docker inspect <container>` to view all details about the container

## Docker create, start, stop, pause, and remove containers
- `docker run` is a stacked command that combines create and start but knowing the commands at a granual level is importan to understand the lifecycle
- the "rootfs" path can be found in inspect container, under "GraphDriver" "MergedDir"
- instead of having to scour through docker inspect you can `docker inspect <container-name> | grep -i <what you're looking for>`

