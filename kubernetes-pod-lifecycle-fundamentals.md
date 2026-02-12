# Kubernetes Pod Lifecycle Fundamentals

- A pod is the smallest kubernetes object used to represent a single instance of an application
- consists of one or more containers sharing network and storage resources
- you can create a pod using a single-line `kubectl` command or apply a tiny YAML manifest
- As always use --help to see all of the commands at your disposal e.g. `kubectl --help`
- In kubernetes, you don't run containers directly, you create pods that contain containers
- To start a pod e.g. Start a nginx pod `kubectl run nginx --image=nginx`
- Another way to start this pod woulkd be a YAML manifest
- e.g `apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  \- name: nginx
    image: nginx`
- To apply the above: `kubectl apply -f pod.yaml`
- To get basic information of you kubernetes pods, use `kubectl get pods`
- to get more info such as IP address, use `kubectl get pods -o wide` this widens the info table
- similar to `docker exec` kubernetes has a `kubectl exec` command allowing you to
- to run a simple command such as finding hostname, you can use `kubectl exec nginx -- hostname`
- this follows the following format: `kubectl exec POD -- COMMAND`
- to print your running pods logs use `kubectl logs <pod_name>`
- use `>` to save the logs to a file e.g `kubectl logs nginx > pods-logs.txt`
- Pods run on specific nodes in the kubernetes cluster
- To see which node your pod is running on use the kubectl command to show pod info
- To delete a pod and clean up your resources, use `kubectl delete pod` e.g. `kubectl delete pod nginx`
