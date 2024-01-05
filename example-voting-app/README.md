---
runme:
  id: 01HKBT3TZQNKN765FJRT1RE1XF
  version: v2.0
---

## Example Voting App Kubernetes

This is based on the original [example-voting-app](https://github.com/dockersamples/example-voting-app) repository from the [docker-examples](https://github.com/dockersamples) GitHub page

and modified it to work on the Kubernetes cluster.

```sh {"id":"01HKBT42VTJ2S9YXS6FH2J2RXW"}
# check all definition files are present
ls -l

# create all deployments and services
kubectl create -f voting-app-deploy.yaml
kubectl create -f voting-app-service.yaml

kubectl create -f redis-deploy.yaml
kubectl create -f redis-service.yaml

kubectl create -f postgres-deploy.yaml
kubectl create -f postgres-service.yaml

kubectl create -f worker-app-deploy.yaml

kubectl create -f result-app-deploy.yaml
kubectl create -f result-app-service.yaml

# check all deployments and services are created
kubectl get all

# get the url of the voting and result service
minikube service voting-service --url
minikube service result-service --url

# scale the voting app to 3 instances
kubectl scale deploy voting-app-deploy --replicas=3
```


