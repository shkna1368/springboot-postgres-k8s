# springboot-postgres-k8s
springboot-postgres-k8s <br/>
before install docker:<br/>
enable hyperv <br/>
disable wsl2 <br/>

install docker desktop: <br/>
in install sisable wsl2 <br/>
in last step,in dialogbox confirm use hayperv <br/>

if docker has problem in startup,enter below command in terminal:

netsh winsock reset

install minikube:
https://github.com/kubernetes/minikube/releases
 minikube-windows-amd64.exe

https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/
kubectl


download  minikube-windows-amd64.exe and kubectl ,copy in same folder.rename  minikube-windows-amd64.exe to minikube.

set environment variable:
edit Path : add C:\minikube

for chcke correctly installed:
minikube version
minikube status

 



open terminal (cmd in windows)
minikube start --driver=docker

read docker image:

minikube docker-env

 @FOR /f "tokens=*" %i IN ('minikube -p minikube docker-env --shell cmd') DO @%i

remove docker image:kubectl
docker  rmi -f image postgres:latest

kubectl get deployment

kubectl delete deployment postgres
kubectl delete service postgres

deploy postgres:
kubectl apply -f postgres-configmap.yml
kubectl apply -f postgres-credentials.yml
kubectl apply -f postgres-deployment.yml
------
login to postgres:
kubectl get pods
kubectl exec -it postgres-6df5844bdd-drvf8 bash
psql -h postgres -U postgres
enter password:postgres
\l  ----->see all databases
\c employeedb  ----->connect to database
exit
exit
-----
clean package project for make jar file

  go to project folder in terminal

make docker image :
docker build -t sp-k8s-db-demo:1.0 .

for see docker images:
docker images

got to deployment file in terminal:
kubectl apply -f deployment.yml
kubectl get pods
kubectl logs springboot-postgres-k8s-ff4f85f95-t5td2


kubectl port-forward svc/springboot-postgres-k8s 8080:8080

open browser :
http://localhost:8080/api/employees

open another terminal:
minikube dashboard
see deployment,service,confihmap,secret and ....



