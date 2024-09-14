FRONT_END_BINARY=frontApp
BROKER_BINARY=brokerApp
LOGGER_BINARY=loggerServiceApp
AUTH_BINARY=authApp
MAIL_BINARY=mailerApp
LISTENER_BINARY=listenerApp

## up: starts all containers in the background without forcing build
up:
	@echo "Starting Docker images..."
	docker-compose up -d
	@echo "Docker images started!"

## up_build: stops docker-compose (if running), builds all projects and starts docker compose
up_build: build_broker build_logger build_listener build_auth build_mail
	@echo "Stopping docker images (if running...)"
	docker-compose down
	@echo "Building (when required) and starting docker images..."
	docker-compose up --build -d
	@echo "Docker images built and started!"

## down: stop docker images
down:
	@echo "Stopping docker compose..."
	docker-compose down
	@echo "Done!"

## build_broker: builds the broker binary a a linux executable
build_broker:
	@echo "Building broker binary..."
	cd ../broker-service && env GOOS=linux CGO_ENABLED=0 go build -o ${BROKER_BINARY} ./cmd/api
	@echo "Done!"

## build_logger: builds the logger binary a a linux executable
build_logger:
	@echo "Building logger binary..."
	cd ../logger-service && env GOOS=linux CGO_ENABLED=0 go build -o ${LOGGER_BINARY} ./cmd/api
	@echo "Done!"

## build_listener: builds the listener binary a a linux executable
build_listener:
	@echo "Building listener binary..."
	cd ../listener-service && env GOOS=linux CGO_ENABLED=0 go build -o ${LISTENER_BINARY} .
	@echo "Done!"

## build_mail: builds the mail binary a a linux executable
build_mail:
	@echo "Building mail binary..."
	cd ../mail-service && env GOOS=linux CGO_ENABLED=0 go build -o ${MAIL_BINARY} ./cmd/api
	@echo "Done!"

## build_auth: builds the auth binary a a linux executable
build_auth:
	@echo "Building auth binary..."
	cd ../authentication-service && env GOOS=linux CGO_ENABLED=0 go build -o ${AUTH_BINARY} ./cmd/api
	@echo "Done!"

## build_front: builds the front end binary
build_front:
	@echo "Building front end binary..."
	cd ../front-end && env CGO_ENABLED=0 go build -o ${FRONT_END_BINARY} ./cmd/web
	@echo "Done!"

## start: starts the front end
start: build_front
	@echo "Starting the front end"
	cd ../front-end && go build -o ${FRONT_END_BINARY} ./cmd/web
	cd ../front-end && ./${FRONT_END_BINARY} &

## stop: stop the front end
stop:
	@echo "Stopping front end..."
	@-pkill -SIGTERM -f "./${FRONT_END_BINARY}"
	@echo "Stopped front end!"

## build images and push to dockerhub:
build_dockerhub: build_dockerhub_broker build_dockerhub_logger build_dockerhub_listener build_dockerhub_mail build_dockerhub_auth build_dockerhub_front
	@echo "Done build all services and push to dockerhub..."


build_dockerhub_broker:
	@echo "Build and tag broker image..."
	cd ../broker-service && docker build -f broker-service.dockerfile -t m3kong/broker-service:1.0.0 .
	docker push m3kong/broker-service:1.0.0
	@echo "Done!"

build_dockerhub_logger:
	@echo "Build and tag logger image..."
	cd ../logger-service && docker build -f logger-service.dockerfile -t m3kong/logger-service:1.0.0 .
	docker push m3kong/logger-service:1.0.0
	@echo "Done!"

build_dockerhub_listener:
	@echo "Build and tag listener image..."
	cd ../listener-service && docker build -f listener-service.dockerfile -t m3kong/listener-service:1.0.0 .
	docker push m3kong/listener-service:1.0.0
	@echo "Done!"

build_dockerhub_mail:
	@echo "Build and tag mail image..."
	cd ../mail-service && docker build -f mail-service.dockerfile -t m3kong/mail-service:1.0.0 .
	docker push m3kong/mail-service:1.0.0
	@echo "Done!"

build_dockerhub_auth:
	@echo "Build and tag mail image..."
	cd ../authentication-service && docker build -f authentication-service.dockerfile -t m3kong/auth-service:1.0.0 .
	docker push m3kong/auth-service:1.0.0
	@echo "Done!"

build_dockerhub_front:
	@echo "Build and tag front-end image..."
	cd ../front-end && docker build -f front-end.dockerfile -t m3kong/front-end:1.0.0 .
	docker push m3kong/front-end:1.0.0
	@echo "Done!"