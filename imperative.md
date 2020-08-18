# Imperative commands

Keeping imperative commands handy is essential for not only CKAD certification exam but also to spin up K8s resources quickly. Below are imperative commands for some of the widely used resources:

 **create a namespace**
```sh
k create ns dev-ns
```

 **Create a pod in dev-ns namespace with label tier=webapp and expose it within cluster. The target port for the service should be 80.**
```sh
kubectl run nginx --image=nginx:alpine -l tier=webapp --port=80 --expose -n dev-ns
```

 **Create a service redis-service to expose the redis application (Pod) within the cluster on port 6379.**
```sh
kubectl expose pod redis --port=6379 --name redis-service	
```

 **create deployment with image nginx and scale to 2**
  ```sh
$ kubectl create deployment webapp --image=nginx
$ kubectl scale deployment/webapp replicas=2
```

