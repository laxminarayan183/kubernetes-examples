# Simple Notes App Using Kubernetes,AWS ubuntu instance

Flow
docker image -> dockerhub push image -> create manifest files -> port forward -> AWS security group

## Steps

1. Build the docker image app
```
docker build -t notes-app .
```
2. Create a access key token in dockerhub to push docker image
3. Push docker image on docker hub
4. create deployment,service,namespace yml file
5. apply all files
```
kubectl apply -f namespace.yml
```
6. To chcek
```
kubectl get pods -n notes-app
```
7. port binding 
```
kubectl port-forward service/notes-app-service -n notes-app 8000:8000 --address=0.0.0.0
```
8. Go to security group add 8000 port
9. copy public ip paste browser with 8000

# For HPA 
1. create hpa file & apply
2. to check cpu utilization
```
kubectl get hpa -n nginx
```
3. to check pods
```
kubectl get pods -n nginx
```
