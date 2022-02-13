# FoodBuzz - A online food devlivery solution



## Assumptions:
- Only operating in Bangladesh
- No govt regulation for deploying the system outside the country border
- Can get up to millions of concurrent users
- Total users can be around 20-30 million
- There would be high traffic throughout the day
- Traffic will be comparatively less during nighttime
- No complex recommendation engine that may require GPU
- Programming languages: Golang, Python, Java, ReactJS, NodeJS
- Message Broker: RabbitMQ, Kafka
- Database: Postgres, MongoDB
- Caching layer: Redis
- Service to service communication techniques: gRPC, REST API
- Code repository: Gitlab
- Object store: S3 compatible solutions

### Summary of overall tools used for the deployment:
- Cloud: Digital Ocean
- Strategy: Managed Kubernetes
- No Of Cluster: 2 (Development and Production)
- GitOps: FluxCD
- Service Mesh: Istio
- Infrastructure as Code: Terraform
- Git Repository: Gitlab
- Loadbalancer: Digital Ocean managed load balancer, Istio Destination rule
- Container registry: Digital Ocean registry
- Database: Managed Postgres, Managed MongoDB
- Object Storage: Digital Ocean Spaces
- Block Storage: Digital Ocean Volumes
- Monitoring, Logging: ElasticSearch, Logstash, Kibana, Grafana, Prometheus, Jaeger, Kiali, Node Exporter

## Brief Details:
As the system is designed in a microservice architecture, the best option is to deploy the system in a managed Kubernetes platform. As this is a food delivery system, there should not be any regulation for deploying the production cluster should be in the cloud and the development cluster can be on-premise.

### Cloud choice: Digitalocean
As we require a managed Kubernetes solution, Digitalocean is a great choice. AWS/GCP also provides managed Kubernetes solutions, but their master plane costs around 72$/m whereas digital ocean is free of cost for the master plane. They only charge for the worker nodes. Besides, we also need the managed Postgres and MongoDB database services. DigitalOcean provides those databases at a lesser cost. They have an S3 compatible object storage system. DigitalOcean provides a load balancer for load balancing the traffics. Also, they have block storage systems. So overall, for this type of project and scale, DigitalOcean is a great choice.

### Infrastructure Definition: Terraform
The whole Digitalocean infrastructure would be defined as IaC (Infrastructure as Code). Terraform can be used for this. It supports DigitalOcean as a provider. There would be two terraform repositories. One for the development cluster and the other for the production cluster. Both the terraform code contains the followings
- Kubernetes cluster resources
- Kubernetes node pool resources
- Loadbalancer definitions
- Firewall resources
- Database resources
- Database replica resources
- Necessary database user resources
- S3 buckets
- VPC resources
- Container registry
- Necessary volumes

### GitOps Strategy:
The whole Kubernetes infrastructure would be defined as GitOps where a git repository would be used for a single source of truth for the whole cluster. We would use the FluxCD tool for this purpose. We create two repositories and attach them with FluxCD. One repository will maintain the production cluster whereas another repository will maintain the development cluster. These repositories will contain necessary deployments, services, service mesh settings, objects stores, PVC, HPA, etc for the clusters. This will help to provision a cluster as a single source of truth. 


### CI/CD Pipeline strategy:
For CI/CD, we can leverage the CI/CD tools of Gitlab and combine them with FluxCD. For the development environment, whenever there is a push in the repository, the CI will be triggered. It will go through the test cases, build the container, push it to the DigitalOcean container registry. And a ImageRespository rule will be written in FluxCD for pulling whenever a new tag is available in the repository. And for production environment, the tag creation would be automated, but the deployment strategy will be manual for safety purpose. 

### Loadbalancing strategy:
For load-balancing, we will use the managed load balancer from DigitalOcean. DigitalOcean provides a highly efficient load balancer at a reasonable cost. Also, we are going to implement a service mesh (Istio) that also makes load balancing the traffic inside the cluster. We will use DigitalOcean's node auto scalar. So our infrastructure nodes will scale automatically based on the load. There will be the use of HPA in the cluster that also can scale pods based on the load inside the cluster.

### Disaster prevention and recovery:
Our cluster will contain redundant nodes that can help to continue the service in case of failure of other nodes. Also, we will use a replica database of the managed database service. That will help protect the data loss in case of disaster. The stateful services may attach the volumes from digital ocean object blocks. So the data is remain safe. For more protection, we can make replication for our database to an on-premise database.


### Logging, alerting, and monitoring:
For logging, we will use the ELK stack which consists of Elasticsearch, Logstash, and Kibana. We can implement a watcher from the ElasticSearch for a particular log notification. Also, Prometheus, jaeger, kiali and grafana will be implemented. Grafana will be able to help visualize the overall success rate and errors from our cluster. Jaeger, kiali will help us monitor service to service communication, the response times, etc. We may also implement Node Exporter with Prometheus which will collect matrices from nodes. These will help visualize the node's RAM, CPU usage, etc in Grafana. We can generate proper alert notifications from Grafana to Slack based on particular rules.

### Certificate and secret management:
For secret management, we can use the HashiCorp vault or sealed secret. This will help to manage the secrets of the cluster. Also, it's possible to rotate the secrets. Also the TLS certificates will be stored in the same way.


