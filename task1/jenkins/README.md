# Spin up jenkins

##### Run jenkins

```bash
docker-compose up -d
```


##### Get initial password and login
```bash
docker exec JenkinsServer cat /var/jenkins_home/secrets/initialAdminPassword

Visit http://[ip]:8090
```

