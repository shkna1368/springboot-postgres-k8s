# springboot-postgres-k8s
springboot-postgres-k8s <br/>
before install docker:<br/>
enable hyperv <br/>
disable wsl2 <br/>

install docker desktop: <br/>
in install sisable wsl2 <br/>
in last step,in dialogbox confirm use hayperv <br/>

if docker has problem in startup,enter below command in terminal: <br/>

netsh winsock reset <br/>

install minikube: <br/>
https://github.com/kubernetes/minikube/releases <br/>
 minikube-windows-amd64.exe <br/>

https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/ <br/>
kubectl <br/>


download  minikube-windows-amd64.exe and kubectl ,copy in same folder.rename  minikube-windows-amd64.exe to minikube. <br/>

set environment variable: <br/>
edit Path : add C:\minikube <br/>

for chcke correctly installed: <br/>
minikube version <br/>
minikube status <br/>

 



open terminal (cmd in windows) <br/>
minikube start --driver=docker <br/>

read docker image: <br/>

minikube docker-env <br/>

 @FOR /f "tokens=*" %i IN ('minikube -p minikube docker-env --shell cmd') DO @%i <br/>

remove docker image:kubectl <br/>
docker  rmi -f image postgres:latest <br/>

kubectl get deployment <br/>

kubectl delete deployment postgres <br/>
kubectl delete service postgres <br/>

deploy postgres: <br/>
kubectl apply -f postgres-configmap.yml <br/>
kubectl apply -f postgres-credentials.yml <br/>
kubectl apply -f postgres-deployment.yml <br/>
------
login to postgres: <br/>
kubectl get pods <br/>
kubectl exec -it postgres-6df5844bdd-drvf8 bash <br/>
psql -h postgres -U postgres <br/>
enter password:postgres <br/> 
\l  ----->see all databases <br/>
\c employeedb  ----->connect to database <br/>
exit <br/>
exit<br/>
----- <br/>
clean package project for make jar file <br/>

  go to project folder in terminal <br/>

make docker image : <br/>
docker build -t sp-k8s-db-demo:1.0 . <br/>

for see docker images: <br/>
docker images

got to deployment file in terminal: <br/>
kubectl apply -f deployment.yml <br/>
kubectl get pods
kubectl logs springboot-postgres-k8s-ff4f85f95-t5td2 <br/>


kubectl port-forward svc/springboot-postgres-k8s 8080:8080 <br/>

open browser : <br/>
http://localhost:8080/api/employees <br/>

open another terminal: <br/>
minikube dashboard <br/>
see deployment,service,confihmap,secret and .... <br/>



