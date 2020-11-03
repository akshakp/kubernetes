Keeping imperative commands handy is essential for not only CKAD/CKA/CKS certification exam but also to spin up K8s resources quickly. Below are imperative commands for some of the widely used resources using kubectl ≥ 1.18:

## Before you start
**Changes in 1.19 version:**
 - "run" commnand will only generate pod. To create all other resources, use "create" command"
 - "--dry-run"  argument available but deprecated hence better start using "--dry-run=client"
 - "--generator" the flag doesn’t work any longer.
 - "k exec pod ls" command is available but deprecated. Better to start using "k exec pod --ls"
 
**Setting up aliases are gifts when clock is ticking faster than you expect

```alias k=kubectl
```
Bonus: export yaml generating command argumemt snippet to save few secods more

```export save="--dry-run=client -o yaml"
```
Example:
***k run nginx --image=nginx $save > nginx.yaml*** will generate nginx.yaml with pod configuration


## Imperative commands

**create a namespace**
```sh
k create ns dev-ns
```

**Create a pod label tier=webapp**
```sh
k run nginx --image=nginx:alpine -l tier=webapp
```

**Create a pod with advance settings**
```sh
k run busybox --image=busybox --limits "cpu=200m,memory=512Mi" --requests "cpu=100m,memory=256Mi" --command -- sh -c "sleep 3600" -o yaml --dry-run=client
```

**Create a deployment**

```sh
k create deployment redis --image=redis --replicas=2
```

**create deployment and scale to 2**
```sh
kubectl create deployment redis --image=redis
kubectl scale deployment/redis --replicas=2
```

**Create configMap**
```sh
kubectl create configmap my-config-map --from-literal=APP_COLOR=green
```

**Create secret**
```sh
kubectl create secret generic app-secret --from-literal=USERNAME=root --from-literal=PASSWORD=Test
```
