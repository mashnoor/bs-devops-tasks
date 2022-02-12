# Install istio service mesh

##### Download Istio

```bash
https://istio.io/latest/docs/setup/getting-started/
```


##### Install Istio

```bash
istioctl install --set profile=demo -y -f istio-operator-config.yaml
```

##### Check if Istio is deployed

```
kubectl get pods -n istio-system
```