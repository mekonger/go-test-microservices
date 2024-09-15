# go-test-microservices
Build an example to learn about the microservices with go languages.

Main system design follow up this diagram
![Go Microservices Diagram](./docs/images/go-microservices.jpg)

## Target
- Breaking monolith up from functions/ packages to completely separate programs
- Communicate via JSON/REST, RPC, gRPC and over a messaging queue
- Easier to scale
- Easier to maintain
- Easier to deploy with Docker Compose, Docker Swarm
  
## What we'll build
A front end web application that connects to 5 Microservices:
- **Broker** - optional single point of entry to micro services
- **Authentication** - Postgres database which authenticate to all other services
- **Logger** - MongoDB which use to log event issue by other services
- **Mail** - sends email with a specific template
- **Listener** - consumes messages in RabbitMQ and initates a process

## Build images for our microservices
- Register account at Dockerhub
- Build images of each service and push to Dockerhub registry with these example commands:
```
docker build -f logger-service.dockerfile -t m3kong/logger-service:1.0.0
docker push m3kong/logger-service:1.0.0
```
- Deploy docker swarm
```docker stack deploy -c swarm.yml myapp```
- Scaling up service ```docker service scale myapp_listener-service=2 ```