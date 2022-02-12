# Task 2

### Setup Cluster
##### Install Virtualbox

```bash
https://www.virtualbox.org/wiki/Downloads
```

##### Install Vagrant
```bash
https://www.vagrantup.com/downloads
```


##### Spin up Vagrant Cluster
```bash
cd cluster
vagrant up
```


##### Deploy Kubernetes Metrics Server and Dashboard
```bash
vagrant ssh master
kubectl apply -f https://raw.githubusercontent.com/mashnoor/bs-devops-tasks/master/task2/deploy/metric-server.yaml
kubectl apply -f https://raw.githubusercontent.com/mashnoor/bs-devops-tasks/master/task2/deploy/kubernetes-dashboard.yaml
```
