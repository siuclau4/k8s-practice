---
runme:
  id: 01HKEVM7GN7FSC3QG5XK8FJ0D1
  version: v2.2
---

```bash {"id":"01HKEVM7GN7FSC3QG5XFWQA82F"}

# set kubectl alias
alias k=kubectl

# short name
csr      	certificatesigningrequests
cs	      componentstatuses
cm	      configmaps
ds	      daemonsets
deploy	  deployments
ep	      endpoints
ev	      events
hpa      	horizontalpodautoscalers
ing	      ingresses
limits	  limitranges
ns	      namespaces
no	      nodes
pvc	      persistentvolumeclaims
pv	      persistentvolumes
po	      pods
pdb	      poddisruptionbudgets
psp	      podsecuritypolicies
rs	      replicasets
rc	      replicationcontrollers
quota	    resourcequotas
sa	      serviceaccounts
svc	      services

# imperative command examples
kubectl get all
kubectl get po -A # all namespaces
kubectl run nginx-pod --image=nginx:alpine
kubectl run redis --image=redis:alpine --labels=tier=db
kubectl run custom-nginx --image=nginx --port=8080
kubectl get redis -o yaml > redis-definition.yaml

kubectl run webapp-green --image=kodekloud/webapp-color -- --color=green
kubectl run webapp-green --image=kodekloud/webapp-color --command -- --color green

kubectl run httpd --image=httpd:alpine
kubectl expose po httpd --type=ClusterIP --port=80

kubectl expose po redis --name=redis-service --port=6379 --type=ClusterIP

kubectl create deploy webapp --image=kodekloud/webapp-color --replicas=3
kubectl create deploy redis-deploy --image=redis --replicas=2 -n=dev-ns

kubectl create ns dev-ns

kubectl create cm custom-cm --from-literal=KEY_1=value_1 --from-literal=KEY_2=value_2

kubectl create ingress -n=critical-space ingress-pay --rule="host/path*=service:8282"

kubectl create role develop --verb=create,delete,list --resource=pods
kubectl create rolebinding dev-user-binding --role=developer --user=dev-user --namespace=default
kubectl create clusterrole custom-role --verb=* --resource=nodes
kubectl create clusterrolebinding custom-rb --clusterrole=custom-role --user=michelle

kubectl create secret tls tls-secret --cert=path/to/tls.cert --key=path/to/tls.key


# contexts
kubectl config get-contexts                          # display list of contexts
kubectl config current-context                       # display the current-context
kubectl config use-context my-cluster-name           # set the default context to my-cluster-name

kubectl config view
kubectl config use-context demo-context
kubectl config use-context research --kubeconfig my-kube-config #use my-kube-config file

# authorization
kubectl describe pod kube-apiserver-controlplane -n kube-system
kubectl get role -A
kubectl describe rolebinding kube-proxy -n kube-system
kubectl auth can-i list pods --as dev-user

kubectl api-resources --namespaced=true
kubectl api-resources --namespaced=false

kubectl exec -n kube-system kube-apiserver-controlplane -- kube-apiserver -h
vi /etc/kubernetes/manifest/kube-apiserver.yaml

# pods
kubectl get pods
kubectl get pods -o wide
kubectl get pods --selector=name=app-name
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

# ConfigMap
kubectl get cm

# Taint
kubectl taint nodes node01 [key]=[value]:[effect]

# Service Account
kubectl get sa
kubectl create token dashboard-sa

# set label for node
kubectl label node node01 color=blue

# logging and monitoring
docker logs -f ecf
kubectl logs -f demo-pod demo-container # stream

minikube addons enable metrics-server

git clone https://github.com/kubernetes-incubator/metrics-server.git
kubectl create -f deploy/1.8+/

kubectl top node
kubectl top po -A

# selector
kubectl get po --selector env=dev,bu=finance

# helm
helm search hub wordpress
helm repo add bitnami https://charts.bitnami.com/bitnami
helm search repo joomla
helm repo ls

helm install devserver nginx-stable/nginx-ingress -n team-yellow
helm install mywebapp ./apache
helm delete devserver
helm ls -A

helm pull bitnami/apache --untar # Download the bitnami apache package under . directory.
helm pull bitnami/apache --untar --untardir /root/test # Download the bitnami apache package under the /root/test directory.

```
