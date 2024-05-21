## case 1
```
kubectl apply -f kube-system/dns.yaml

kubectl get configmaps --namespace=kube-system coredns -o yaml

kubectl -n kube-system rollout restart deployment coredns
```
## case 2
```
kubectl get configmap coredns -n kube-system -o yaml | sed '/log/i \ \ \ \ rewrite name regex (.*)\\.aimerzarashi\\.com istio-ingressgateway.istio-system.svc.cluster.local' | kubectl apply -f -

kubectl -n kube-system rollout restart deployment coredns
```