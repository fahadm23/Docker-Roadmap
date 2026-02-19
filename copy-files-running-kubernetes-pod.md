# Copy Files To/From a Running Kubernetes Pod
- When using `kubectl cp`, you need to specify which pod you're copying to/from. The pod name needs to be part of the path\
- # Copy TO a pod
`kubectl cp <local-file> <pod-name>:<path-in-pod>`

- # Copy FROM a pod
`kubectl cp <pod-name>:<path-in-pod> <local-file>`

- If a pod has multiple containers, you need to specify which one:
- `kubectl cp ~/nginx.conf <POD-NAME>:<PATH> -c <CONTAINER-NAME>`
- To trigger a config reload and update the pod with the file, use `kubectl exec web -- nginx -s reload`
