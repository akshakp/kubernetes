Keeping imperative commands handy is essential for not only CKAD/CKA/CKS certification exam but also to spin up K8s resources quickly. Below are imperative commands for some of the widely used resources using kubectl ≥ 1.18:

## Before you start
**Changes in 1.19 version:**
 - "run" commnand will only generate pod. To create all other resources, use "create" command
 - "--dry-run"  argument available but deprecated hence better start using "--dry-run=client"
 - "--generator" the flag doesn’t workubectl any longer.
 - "kubectl exec pod ls" command is available but deprecated. Better to start using "kubectl exec pod --ls"
 
**Setting up alias is a gift when clockubectl is ticking faster than you expect**

```sh
alias k=kubectl
```
> Bonus: export yaml generating command argumemt snippet to save few more secods.

```sh
export save="--dry-run=client -o yaml"
```
Example:
> ***kubectl run nginx --image=nginx $save > nginx.yaml*** will generate nginx.yaml with pod configuration


## Short names for api resources
You would thank yourself for mastering the short names of resources:

|Resource Name              |short name      	|
|---------------------------|-------------------|
|namespaces        			|`ns`				|
|Pods			  			|`po`				|
|deployments       			|`deploy`			|
|services		  			|`svc`				|
|configmaps		  			|`cm`				|
|cronjobs					|`cj`				|
|nodes			  			|`no`				|
|persistentvolumes 			|`pv`				|
|persistentvolumeclaims		|`pvc`				|
|replicasets				|`rs`				|
|ingresses					|`ing`            	|
|networkpolicies			|`netpol`			|
|daemonsets					|`ds`				|
|endpoints					|`ep`				|
|replicasetcontrollers		|`rs`				|
|serviceaccounts   			|`sa`				|
|storageclasses				|`sc`				| 

 > ***`kubectl api-resources`*** will provide the up-to date list of api resources short names  


## Imperative commands

**create a namespace**
```sh
kubectl create ns dev-ns
```

**Create a pod label tier=webapp**
```sh
kubectl run nginx --image=nginx:alpine -l tier=webapp
```

**Create a pod with advance settings**
```sh
kubectl run busybox --image=busybox --limits "cpu=200m,memory=512Mi" --requests "cpu=100m,memory=256Mi" --command -- sh -c "sleep 3600" -o yaml --dry-run=client
```
**Update pod/container configuration/property**
```sh
kubectl get pod busybox -o yaml > busybox.yaml
```

> Update/correct a container image, activeDeadlineSeconds or pod tolerations in running pod can be performed inline with **kubectl edit pod** command.
```sh
kubectl edit pod <podname>
```

**Create a deployment**

```sh
kubectl create deployment redis-deployment --image=redis --replicas=2
```

**Scale deployment to 5 replicas**
```sh
kubectl scale deployment/redis-deployment --replicas=5
```

**Update container image in deployment**

```sh
kubectl set image deployment.v1.app/redis-deployment redis=redis:alpine
```

**Update container resources in deployment**
```sh
kubectl set resources deployment.v1.apps/redis-deployment -c=redis --limits=cpu=200m,memory=512Mi
```

> Or if you prefer declarative way, you can easily edit any field/property of the POD template. Since the pod template is a child of the deployment specification,  with every change the deployment will automatically delete and create a new pod with the new changes. So if you want to edit a property of a POD part of a deployment you may do that simply by running the command
```sh
kubectl edit deployment <deploymentname>
```

**Create configMap**
```sh
kubectl create configmap my-config-map --from-literal=APP_COLOR=green
```

**Create secret**
```sh
kubectl create secret generic app-secret --from-literal=USERNAME=root --from-literal=PASSWORD=Test
```
