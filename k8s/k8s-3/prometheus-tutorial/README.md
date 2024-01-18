# Prometheus installation
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```
```
helm install my-monitoring prometheus-community/kube-prometheus-stack
```
### Explore installation components
```
kubectl get all
kubectl get cm
kubectl get secrets
```
### Let's start by review kube-state metrics
```
kubectl port-forward --address 0.0.0.0 svc/my-monitoring-kube-state-metrics 8080:8080
```
### in browser localhost:8080, explore metrics
---
### Next let's port-forward and explore prometheus UI
```
kubectl port-forward --address 0.0.0.0 svc/my-monitoring-kube-prometh-prometheus 8080:9090
```
### in browser localhost:8080, go to Status, explore Service Discovery, Targets, Rules and Configuration tabs 
### execute PromQL examples queries https://prometheus.io/docs/prometheus/latest/getting_started/#using-the-expression-browser

```
kubectl port-forward --address 0.0.0.0 svc/my-monitoring-grafana 8081:80
```
### User/Password: admin/prom-operator
### Explore dashboards, Grafana configuration etc,.
### Explore values.yaml
```
helm pull prometheus-community/kube-prometheus-stack
tar xvf kube-prometheus-stack-45.9.1.tgz
cd kube-prometheus-stack
```
### Take time to review values.yaml

### JMX-exporter (PodMonitor, ServiceMonitor CRD)
```
cd jmx-exporter-kubernetes
docker build -t fayfa/jmx:v3 .
cd manifests
kubectl apply -f .
kubectl get pods -o wide
```
#### copy IP for tomcat and paste it in line 6 at values.yaml
#### Update prometheus:
```
helm upgrade --install my-monitoring prometheus-community/kube-prometheus-stack -f value.yaml
```
#### Check in Prometheus UI target java is apper
#### Let's add dashboard in Grafana
#### Go to dashboards and add new dashboard and import 8563





### Uninstall prometheus:
```
helm uninstall my-monitoring
kubectl delete crd alertmanagerconfigs.monitoring.coreos.com
kubectl delete crd alertmanagers.monitoring.coreos.com
kubectl delete crd podmonitors.monitoring.coreos.com
kubectl delete crd probes.monitoring.coreos.com
kubectl delete crd prometheuses.monitoring.coreos.com
kubectl delete crd prometheusrules.monitoring.coreos.com
kubectl delete crd servicemonitors.monitoring.coreos.com
kubectl delete crd thanosrulers.monitoring.coreos.com
```



```
https://artifacthub.io/packages/helm/prometheus-community/kube-prometheus-stack

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack
```