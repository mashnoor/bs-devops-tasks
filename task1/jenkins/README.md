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



##### Set Dockerhub credentials
- Login to jenkis
- Go to Manage Jenkins
- Go to Manage Credentials
- Go to Jenkins credentials store
- Go to Global credentials
- Hit Add Credentials
- Add your dockerhub username, password and set ID=dockerhub
- Hit ok and done

##### Set Docker plugin
- Login to jenkis
- Go to Manage Jenkins
- Go to Manage Plugins
- From Available tab search for 'Docker Pipeline' plugin and install