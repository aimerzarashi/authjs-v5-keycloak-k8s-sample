## install
``` 
minikube start --memory='6g' --cpus=8 mount /data:/data
 
istioctl install --set profile=demo -y
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/kiali.yaml
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/grafana.yaml
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/jaeger.yaml
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/prometheus.yaml
 
kubectl rollout status deployment/kiali -n istio-system
kubectl rollout status deployment/grafana -n istio-system
kubectl rollout status deployment/jaeger -n istio-system
kubectl rollout status deployment/prometheus -n istio-system
 
istioctl dashboard kiali
 
minikube tunnel

kubectl create -n istio-system secret tls tls-credential-aimerzarashi.com --key=tls/aimerzarashi.com/privkey1.pem --cert=tls/aimerzarashi.com/fullchain1.pem 

kubectl apply -f _k8s/kube-system/dns.yaml
kubectl -n kube-system rollout restart deployment coredns

kubectl create namespace services
kubectl label namespace services istio-injection=enabled --overwrite
kubectl apply -n=services -f _k8s/
``` 

## uninstall
``` 
kubectl delete -n=services -f _k8s/
kubectl delete namespace services
 
kubectl delete -n istio-system secret tls-credential-aimerzarashi.com

kubectl delete -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/kiali.yaml
kubectl delete -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/grafana.yaml
kubectl delete -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/jaeger.yaml
kubectl delete -f https://raw.githubusercontent.com/istio/istio/release-1.21/samples/addons/prometheus.yaml
kubectl delete namespace istio-system
 
minikube delete
``` 