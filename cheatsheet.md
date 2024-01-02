kubectl get all

# pods

kubectl get pods
kubectl get pods -o wide
kubectl describe pod [pod-name]
kubectl run [pod-name] --image=[image-name]
kubectl create -f [filename]
kubectl apply -f [filename]
kubectl run [pod-name] --image=[image-name] --dry-run=client -o yaml > [filename]

# replication-controllers

kubectl get replicationcontrollers
kubectl get replicationcontrollers -o wide
kubectl describe replicationcontroller [replicationcontroller-name]

# replica-set

kubectl get replicasets
kubectl get replicasets -o wide
kubectl describe replicasets [replicasets-name]
kubectl edit replicasets [replicasets-name]
kubectl scale replicas=[replica-num] replicasets nginx
kubectl scale replicas=[replica-num] rs/nginx

# deployment

kubectl get deployments
kubectl get deployments -o wide
kubectl create -f [filename] --record
kubectl apply -f [filename]
kubectl rollout status deployment/[deployment-name]
kubectl rollout history deployment/[deployment-name]
kubectl rollout undo deployment/[deployment-name]
kubectl edit deployment [deployment-name]
kubectl set image deployment [container-name]=[image-name:version] --record
