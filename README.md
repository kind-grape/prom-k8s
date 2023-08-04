# prom-k8s
## Prometheus and Grafana related deployment workflow

### Create Prometheus and Grafana Custome Image if requried
```
#make sure valid docker file in the directory 
docker build . 
```

### Create Auxilary Resources for Deployments/Statefulset 
1. Create prometheus config map
   ```
   oc apply -f prom-conf-cm.yaml
   ```

1. Create grafana datasource conf config map or secret  
  ***note***
  grafana datasource has now been updated as a secret object as now it contains the SA token to interact with the cluster Prometheus  
  please refer to the `grafana_sa.yaml` file for more context
  
   ```
   oc apply -f grafana-datasource-conf-cm.yaml
   or 
   oc apply -f grafana-datasource-cm-secret.yaml
   ```

1. Create the grafana role for pulling metrics from local cluster Prometheus. Refer to `grafana_sa.yaml` for instruction

1. Create grafana dashboard conf config map 
   ```
   oc apply -f grafana-datasource-cm.yaml
   ```

1. Create vault grafana dashboard config map 
   ```
   oc apply -f grafana-vault-dashboard-cm.yaml
   ```

1. Create network service for Premethues, which would be used by Grafana
   ```
   oc apply -f network.yaml
   ```


1. Create statefulset 
   ```
   oc apply -f statefulset.yaml
   ```

### Port forward Prometheus container
  ```
  oc port-forward {prom-pod-name} 8080:9090
  ```

### Port forward grafana container 
```
oc port-forward {grafana-pod-name} 3000
```
