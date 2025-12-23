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

## Run containers overriding default command
- Some docker containers include more than one executable file
- e.g. running `docker run redis` will start a redis server but also includes the redis-cli executable which you can use without installing it on your machine if you know how to override the default command
- To run the redis-cil: `docker run redis redis-cli --version`
- where `docker run` = BASE COMMAND
- `redis` = IMAGE
- `redis-cli --verion`: the COMMAND and ARG that override the default redis-server
- `docker run redis redis-cli -h 172.16.0.3 ping` will run the redis server and connect to the address given using the cli
- ### Visual breakdown:
docker run    redis         redis-cli -h 172.16.0.3 ping
    ↓           ↓                      ↓
Docker      Image         Command + Arguments
command     name          (overrides default)
- In a situation where you need to work with redis, instead of installing it on your machine and other tools that are needed, you can use a redis container image
- This saves time by providing an already configured environment

## Run CLI tools in containers (interactive mode)
- We will be storing an image on a redis database on a remote server
- the image is avatar.png
- Redis is a key-value database
- we will store the image with the kay name `avatar:user123`
- `cat ~/avatar.png | redis-cli -h HOST -p PORT -x set avatar:user123`
- `cat ~/avatar.png` - reads the file and outputs its contents
- `|` - pipe symbol, sends that output to the next command
- `redis-cli -h HOST -p PORT` - connect to Redis server at HOST:PORT
- `-x` - tells redis-cli to read the VALUE from STDIN (the piped data)
- `set avatar:user123` - Redis command that sets a key called avatar:user123
- the `-i` interactive command keeps the containers STDIN open standard input
- standard input is like a receiving inbox
- what we did is read the image content (avatar.png), | pipe it onto the redis container, gave it the -h host and -p port of where we want to send it, then used -x to read the piped data and store it to the key value pair avatar:user123

## Run shells in containers (TTY-controlled mode)
- the -t flag `docker run -t` allocates a pseudo terminal that controls the containerized application
- this allows terminal size detection, coloured output, cursor control, terminal specific signals
- You may need to use this for running interactive shells, language REPLs (read, evaluate, print, loop) and text editors
- a normal terminal wont be able to properly display these
- TTY controlled

## Run containers with arbitrary endpoints
- To change the entrypoint of a container, use the --entrypoint flag followed by the argument
- e.g. to open an interactive shell `docker run --entrypoint sh -it alpine/httpie`
- This can be used if you want to run a shell instead of execute the binary
- the interactive shell allows you to explore the containers filesystem and contents
- explore, debug why a container isn't working
  

## Pass environment variables to containers
- Containerized applications run in isolated environments, which means your envs will not be available to the system
- This is done for security purposes
- e.g. `docker run -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=1234 postgres`
- reminder: `docker run [ALL_DOCKER_OPTIONS] IMAGE [COMMAND_TO_RUN_IN_CONTAINER]`
- you need to use a separate -e flag for each env
- you can also store the variables in a file and pass it to the container using the `--env-file` flag


