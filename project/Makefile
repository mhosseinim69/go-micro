# Use Windows shell
SHELL=cmd.exe

# Binary names
FRONT_END_BINARY=frontApp.exe
BROKER_BINARY=brokerApp
AUTH_BINARY=authApp
LOGGER_BINARY=loggerServiceApp
# ==============================
# Docker commands
# ==============================

## up: start all containers in the background
up:
	@echo Starting Docker images...
	docker-compose up -d
	@echo Docker images started!

## up_build: stop containers, build everything, and start again
up_build: build_broker build_auth build_logger
	@echo Stopping Docker images (if running)...
	docker-compose down
	@echo Building and starting Docker images...
	docker-compose up --build -d
	@echo Docker images built and started!

## down: stop docker-compose
down:
	@echo Stopping Docker compose...
	docker-compose down
	@echo Done!

# ==============================
# Build commands
# ==============================

## build_broker: build broker as Linux binary (for Docker)
build_broker:
	@echo Building broker binary...
	cd ..\broker-service && set GOOS=linux&& set GOARCH=amd64&& set CGO_ENABLED=0&& go build -o $(BROKER_BINARY) ./cmd/api
	@echo Done!

## build_logger: build logger as Linux binary (for Docker)
build_logger:
	@echo Building logger binary...
	cd ..\logger-service && set GOOS=linux&& set GOARCH=amd64&& set CGO_ENABLED=0&& go build -o $(LOGGER_BINARY) ./cmd/api
	@echo Done!

## build_auth: build auth as Linux binary (for Docker)
build_auth:
	@echo Building auth binary...
	cd ..\authentication-service && set GOOS=linux&& set GOARCH=amd64&& set CGO_ENABLED=0&& go build -o $(AUTH_BINARY) ./cmd/api
	@echo Done!

## build_front: build front-end as Windows binary
build_front:
	@echo Building front end binary...
	cd ..\front-end && set CGO_ENABLED=0&& set GOOS=windows&& go build -o $(FRONT_END_BINARY) ./cmd/web
	@echo Done!

# ==============================
# Front-end runtime commands
# ==============================

## start: build and start the front-end
start: build_front
	@echo Starting front end...
	cd ..\front-end && start /B $(FRONT_END_BINARY)

## stop: stop the front-end
stop:
	@echo Stopping front end...
	@taskkill /IM "$(FRONT_END_BINARY)" /F
	@echo Front end stopped!
