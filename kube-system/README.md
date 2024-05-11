```
kubectl apply -f kube-system/dns.yaml

kubectl get configmaps --namespace=kube-system coredns -o yaml

kubectl -n kube-system rollout restart deployment coredns
```