## Simple Mysql with statefulset 

## Steps
1. create namespace.yml service.yml statfulset.yml files
2. apply it 
```
kubectl apply -f namespace.yml -f service.yml -f statfulset.yml
```
3. to check
```
kubectl get pods -n mysql
```
4. enter in pod 
```
kubectl exec -it mysql-statefulset-0 -n mysql -- bash
```
5. give sql credentials 
```
mysql -u root -p
```
6. delete a pod to test
```
kubectl delete pod mysql-statefulset-0 -n mysql
```
7. It will recreate same pod with same name
