#### I had installed Kiali, Prometheus and Grafana compatible with Istio release-1.24

You can refere below provided helm command and kubernetes manifests to Install Istio and Addons Kiali, Prometheus and Grafana

```
helm repo add istio https://istio-release.storage.googleapis.com/charts
helm repo update

kubectl create ns istio-system
helm install istio-base istio/base -n istio-system 
helm install istiod istio/istiod -n istio-system
helm install istio-ingressgateway istio/gateway -n istio-system 
helm install istio-egressgateway istio/gateway -n istio-system

cat server.crt intermediate1.crt intermediate2.crt root.crt > tls.crt
kubectl create secret generic cacerts -n istio-system --from-file=server.crt --from-file=tls.key --from-file=root.crt --from-file=tls.crt

kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/addons/kiali.yaml
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/addons/prometheus.yaml
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/addons/grafana.yaml
```
