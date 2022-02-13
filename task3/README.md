# FoodBuzz - A online food devlivery solution


## Deployment strategies

Assumptions:
Only operating in Bangladesh
No govt regulation for deploying the system outside the country border
Can get up to millions of concurrent users
Total users can be around 20-30 million
There would be high traffic throughout the day
Traffic will be comparatively less during nighttime
Technologies used:
Programming languages: Golang, Python, Java, ReactJS, NodeJS
Message Broker: RabbitMQ, Kafka
Database: Postgres, MongoDB
Caching layer: Redis
Service to service communication techniques: gRPC, REST API
Code repository: Gitlab
Object store: S3 compatible solutions


As the system is designed in a microservice architecture, the best option is to deploy the system in a managed Kubernetes platform. As this is a food delivery system, there should not be any regulation for deploying the production cluster should be in the cloud and the development cluster can be on-premise.

Cloud choice: Digitalocean
Why: As we require a managed Kubernetes solution, Digitalocean is a great choice. AWS/GCP also provides managed Kubernetes solutions, but their master plane costs around 72$/m where digital ocean is free of cost for the master plane. They only charge for the worker nodes. Besides, we also need managed Postgres and MongoDB. Digital ocean provides those databases at a lesser cost. They have an S3 compatible object storage system. Digital ocean provides loadbalancer for load balancing the traffics.

Infrastructure Define:
The whole Digitalocean infrastructure would be defined as IaC (Infrastructre as Code). Terraform can be used for this. It supports digital ocean provider. There would be two terraform respository. One for the development cluster and other for the production cluster. Both the terraform code contains the followings
Kubernetes definitions
Kubernetes node pool definitions
Loadbalancer definitions
Firewall resources
Database resources
Database replica resources
Necessary database user resources
S3 buckets
VPC resources

