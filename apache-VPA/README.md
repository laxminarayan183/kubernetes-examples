# Deployed apache using VPA
Steps
1. Clone git repo
```
git clone https://github.com/kubernetes/autoscaler.git
```
2. change directory
```
cd autoscaler/vertical-pod-autoscaler/
```
3. run command
```
./hack/vpa-up.sh
```
4. cretae vpa yml file & apply
5. port forward
```
sudo -E kubectl port-forward service/apache-service -n apche 82:80 --address=0.0.0.0
```
6. run load generator
```
kubectl run -i --tty load-generator --image=busybox -n apache /bin/sh
```
```
while true; do wget -q -O- http://apache-service.apache.svc.cluster.local; done
```
7. to check
```
watch kubectl get vpa -n apache
```
8. to check cpu utilization
```
kubectl top pod -n apache
```