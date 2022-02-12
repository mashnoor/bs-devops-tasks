
# Task 1

##### Install Docker


```bash
https://docs.docker.com/get-docker/
```




##### Install Minikube


```bash
https://minikube.sigs.k8s.io/docs/start/
```

##### Install Kubectl


```bash
https://kubernetes.io/docs/tasks/tools/
```


##### Start 3 node minikube cluster

```bash
minikube start --nodes 3 -p bs-cluster
```


##### Taint the nodes

```bash
kubectl taint nodes bs-cluster node=master:NoSchedule
kubectl taint nodes bs-cluster-m02 app-name=bs-app1:NoSchedule
kubectl taint nodes bs-cluster-m03 app-name=bs-app2:NoSchedule
```



##### Deploy applications and services

```bash
kubectl apply -f task1/app1/deploy -f task1/app2/deploy
```