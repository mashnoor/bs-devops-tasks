
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




##### Build applications with jenkins

- Login to jenkins by visiting http://[ip]:[port]
- New Item > (Enter name and select Multibranch Pipeline)
- From Branch Sources, select a soucre and enter the public repository url
- From Build Configuration, change the script path to task1/app1/Jenkinsfile 
- Create a new build pipeline for app2. The process is identical to the above one. Chnage the script path to task1/app1/Jenkinsfile
- Hit save and jenkins should automatically clone the repository, build 






#####  Deploy applications
Update image tags in task1/app1/deploy/deployment.yaml and task1/app2/deploy/deployment.yaml

```bash
kubectl apply -f task1/app1/deploy -f task1/app2/deploy
```

