# Profiles rest server.

This is REST practice. Using python3.9.

## Install python3.9(Ubuntu/Debian)
```bash
make install_python3.9
```

## Requirements
For installing requirements:
```bash
make requirements
```

## Worker
To run RabbitMQ worker
```bash
RUN_ARGS="--host localhost --port 5672 --queue rabbitmqqueue" make worker
```

## Server
To run REST server
```bash
RUN_ARGS="--host 0.0.0.0 --port 8000 --rabbitmq_host localhost --rabbitmq_port 5672 --rabbitmq_queue rabbitmqqueue" make server
```
And use `0.0.0.0:8000/docs` to test it. Do not test `users/characters/{username}` on this site, use:
```bash
curl -X 'GET' \
  'http://0.0.0.0:8000/users/characters/{username}' \
  -H 'accept: application/pdf' --output profile.pdf
```

## Docker image
To start the RabbitMQ, REST server and one worker you can use Docker image:
```bash
docker run --rm -it -p 15672:15672 -p 8000:8000 ch0p1k/profiles-rest-server:latest
```
To run in backend process - add `-d` flag

### Account for Rabbit MQ monitoring
Rabbit MQ monitoring: `http://localhost:15672/`
```
login: username
password: username
```
