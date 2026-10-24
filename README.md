# Howest Prime Test Environment

This repository contains a Docker Compose environment for running the Howest Prime web clients and backend services with test dependencies.

## Services

The compose stack includes:

- The Movies service and a PostgreSQL database.
- The Ticketing service and a MongoDB 7 database configured as a replica set.
- LavinMQ as the AMQP message broker.
- The web app and backoffice containers.

The service containers depend on healthy database and broker containers where configured. Docker volumes are used for database persistence between container restarts.

## Start the environment

Install Docker with the Compose plugin. Before starting the stack, make sure the referenced local environment files are present and populated with test-only configuration, and that the required service images are available to Docker.

From this repository root, start the compose project with:

```sh
docker compose -f howestprime-test/docker-compose.yml up -d
```

To stop the containers while retaining named database volumes:

```sh
docker compose -f howestprime-test/docker-compose.yml down
```

Do not put production credentials in this test environment or commit secret values. The compose file and environment files define local service configuration; review them before exposing any ports beyond your development machine.

## API checks

The `http_requests/` directory is reserved for HTTP request examples. Add local `.http` files there to exercise the running APIs.

## Related repositories

- [Movies microservice](https://github.com/Howest-Prime/st-microservice-movies)
- [Ticketing microservice](https://github.com/Howest-Prime/st-microservice-ticketing)
