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

##### Install Ansible
```bash
https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
```


##### Spin up Vagrant and 3 node Kubernetes Cluster
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
