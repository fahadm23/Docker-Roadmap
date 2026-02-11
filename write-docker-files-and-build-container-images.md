## Build and publish a container image with Docker
- Use `docker build --help` to see all docker build commands
- To build a docker image, use `docker build <project path>` e.g. `docker build ~/projects/foobar`
- This builds the image, but to tag it with the name that you want use the `-t` tag followed by the name
- e.g `docker build -t registry.iximiuz.com/foobar:v1.0.0 ~/projects/foobar`
- if the registry required a login before pushing the image, use `docker login <registry address>`
- e.g. `docker login registry.iximiuz.com` you will be prompted for a username and password
- After successfully logging in, you can push the image use `docker push <image name>`
- e.g. `docker push registry.iximiuz.com/foobar:v1.0.0`
- Workflow: **Code → Dockerfile → Build Image → Push to Registry → Deploy Anywhere**
- In a company, dev, staging, and production may pull from the same registry but use different tags

### Basic build
docker build -t myapp:v1 .

### Build from specific Dockerfile
docker build -f Dockerfile.prod -t myapp:prod .

### Build with build arguments
docker build --build-arg NODE_ENV=production -t myapp:v1 .

### Build without cache (fresh build)
docker build --no-cache -t myapp:v1 .

### Multi-platform build (for ARM and x86)
docker buildx build --platform linux/amd64,linux/arm64 -t myapp:v1 .

### Build and output build logs
docker build -t myapp:v1 . 2>&1 | tee build.log

### List local images
docker images

### See image history (layers)
docker history myapp:v1

### Inspect image details
docker inspect myapp:v1

### See image size
docker images myapp:v1 --format "{{.Size}}"

### Remove images
docker rmi myapp:v1
docker image prune  # Remove dangling images
