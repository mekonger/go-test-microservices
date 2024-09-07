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
