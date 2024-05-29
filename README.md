# Fullnode for Penumbra Testnet

## Context

This project aims to create a robust infrastructure using Docker for a [fullnode](https://guide.penumbra.zone/node.html) on the latest Penumbra testnet with a monitoring and alerting system.

In order to implement our setup for fullnode and monitoring. We will be choosing the following technologies:

- Ansible: Automate configurations
- Docker: Containerize all resources
- Prometheus and Grafana: For monitoring

## Implementation

See [infra/README.md](./infra/README.md)

## Acknowledgment

This project was mainly based on the provided resources from [Penumbra Community](https://penumbra.zone/)

* [Penumbra documentation](https://guide.penumbra.zone/node.html)
* [Penumbra deployments](https://github.com/penumbra-zone/penumbra/tree/main/deployments)
* [Penumbra-testnet](https://grpc.testnet.penumbra.zone)
