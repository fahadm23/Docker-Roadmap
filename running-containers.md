# Running Containers
- To run nginx container use `docker run nginx`
- Unlike other containers, this may not self-exit, use Ctrl+C to exit
- Hello-world and nginx containers are instaleld from the official docker hub registry, you can install a container to use another registry
- using e.g. `docker run registry.iximiuzlabs.com`
- short image names are pulling from a longer image address but still work

## Run a Container in Background, Read Logs, and Attach
- when you run a container without any additional flags, it gets ran in the forground and you are not able to use the terminal
- Most of the time, you will want to run the container in the background using the `-d` flag
- This allows you to continue using the terminal with the container still running, and exiting the terminal will not terminate the container
- `docker run` is a compound command that is doing the following: image pull - container create - container attach - network connect - container start
- to list all running containers, use `docker ps`
- to access container logs use `docker logs <container id or name>`
- To attach to a container and have it run in the foreground, use `docker attach <container id or name>`
- 

## Pause and Unpause Containers
- You may need to pause a container during peak hours to allocate resources, or when troubleshooting
- To run a container in the background, use the -d flag
- Running a container without this flag, puts you in attached mode which allows you to see all the outputs
- the `--name` flag allows you to give a name to the container identifier or url, allowing you to call it easier
