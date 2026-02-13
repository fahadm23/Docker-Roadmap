# Deploy a pod with a container image from a private registry

- When using a private registry, you may need to provide credentials
- We did this in docker using `docker login <registry address>`
- There are a few different approaches to doing this in kubernetes
- you can create a yaml, a dockerfile, or doing it straight through the terminal (not recommended for security purposes)
- In the terminal you can use `kubectl create secret docker-registry`
- Followed by your details e.g. `kubectl create secret docker-registry registry-credentials \
  --docker-server=registry.iximiuz.com \
  --docker-username=iximiuzlabs \
  --docker-password='rules!'`
- Then, to run the pod using the image, you will need to create a YAML with the full image path from the registry, your secret file name, etc.
- e.g. `apiVersion: v1
kind: Pod
metadata:
  name: nginx-1
spec:
  containers:
   name: nginx-alpine
    image: registry.iximiuz.com/nginx:alpine
  imagePullSecrets:
   name: registry-credentials`
  - To apply this and run the pod, use `kubectl apply -f pod.yaml`
  
