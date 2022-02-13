
# Task 1

##### Install Docker

https://docs.docker.com/get-docker/



##### Install Minikube

https://minikube.sigs.k8s.io/docs/start/


##### Install Kubectl



https://kubernetes.io/docs/tasks/tools/



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


##### Setup service mesh


https://github.com/mashnoor/bs-devops-tasks/blob/master/task1/infra/README.md


##### Create namespace and inject istio

```bash
kubectl apply -f task1/infra/namespaces.yaml
```

##### Install mesh gateway and nginx virtual service

```bash
kubectl apply -f task1/infra/gateway/ -f task1/infra/virtualservice/
```

##### Setup nginx

https://github.com/mashnoor/bs-devops-tasks/blob/master/task1/nginx/README.md


##### Setup jenkins


https://github.com/mashnoor/bs-devops-tasks/blob/master/task1/jenkins/README.md


##### Build applications with jenkins

- Login to jenkins by visiting http://[ip]:[port]
- New Item > (Enter name and select Multibranch Pipeline)
- From Branch Sources, select a soucre and enter the public repository url
- From Build Configuration, change the script path to task1/app1/Jenkinsfile 
- Update Jenkinsfile if necessary
- Create a new build pipeline for app2. The process is identical to the above one. Chnage the script path to task1/app2/Jenkinsfile
- Hit save and jenkins should automatically clone the repository, build 






#####  Deploy applications
Update images in task1/app1/deploy/deployment.yaml and task1/app2/deploy/deployment.yaml

```bash
kubectl apply -f task1/app1/deploy -f task1/app2/deploy
```

