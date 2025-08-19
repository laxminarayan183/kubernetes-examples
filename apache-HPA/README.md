## Deployed apache using HPA 

- To perform you need metrics 
- if you have minikube - `minikube addons enable mterics-server`  run this command
- if you have kind cluster
  1. `kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml`
  2. `kubectl -n kube-system edit deployment metrics-server`
  3. add container args `--kubelet-insecure-tls`
                        `--kubelet-preferred-address-types=InternalIP,Hostname,ExternalIP`
  4.   restart deployment `kubectl -n kube-system rollout restart deployment metrics-server`
 to check `kubectl top node`

Steps
1. create namespace,deployment,service,hpa file and apply it
2. port forward
```
sudo -E kubectl port-forward service/apache-service -n apche 82:80 --address=0.0.0.0
```
3. generate load on apche server to test

```
kubectl run -i --tty load-generator --image=busybox -n apache /bin/sh
```
```
while true; do wget -q -O- http://apache-service.apache.svc.cluster.local; done
```
4. check cpu utilization
```
kubectl get hpa -n apache
``` 
```
kubectl get pods -n apache
```