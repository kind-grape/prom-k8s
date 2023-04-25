# prom-k8s
Prometheus and Grafana related deployment 

Port forward Prometheus container
```
oc port-forward {prom-pod-name} 8080:9090
```

Port forward grafana container 
```
oc port-forward {grafana-pod-name} 3000
```