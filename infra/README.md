# Infrastructure

## Prerequisites

### Install binaries

- Ansible [installed](http://docs.ansible.com/ansible/intro_installation.html) to automate deployments.
- Docker [installed](https://docs.docker.com/engine/install/) to build images.

### SSH access

To simplify ssh access please add this to your ~/.ssh/config, replace x.x.x.x and y.y.y.y with your IPs:

```bash
# fullnode-0
Host fullnode-0 x.x.x.x
    HostName x.x.x.x
    IdentityFile ${YOUR_PRIVATE_KEY}
    User root

# monitoring
Host monitoring y.y.y.y
    HostName y.y.y.y
    IdentityFile ${YOUR_PRIVATE_KEY}
    User root
```

Note that we are working with bare metal servers, and we will be using root access one time only in order to set our users. It is highly recommended to avoid using root access when possible.

## Usage

### Setup users

We will create some users that we will use for future access and operations for both fullnode-0 and monitoring.

```sh
cd ~/projects
clone git@github.com:0xawaz/awaz-penumbra-testnet.git
cd awaz-penumbra-testnet/infra
```

- dryrun:

```sh
ansible-playbook -i inventory users.yml --check
```

- apply:

```sh
ansible-playbook -i inventory users.yml
```

### Fullnode

In fullnode-0 we will install Penumbra fullnode with its full configuration.

```sh
ansible-playbook -i inventory fullnode.yml --check
ansible-playbook -i inventory fullnode.yml
```

Now our fullnode is up and running.

Let's join Penumbra testnet:

```sh
ssh awaz@fullnode-0
sudo docker exec -it pd-node0 bash
pd testnet unsafe-reset-all
pd testnet join
```

The fullnode wil be syncing, After few hours, make sure fullnode is synced to the [latest block](https://grpc.testnet.penumbra.zone/).

### Monitoring

```sh
ansible-playbook -i inventory monitoring.yml --check
ansible-playbook -i inventory monitoring.yml
```

Now our monitoring is up and running. Now you can:

- Check if Penumbra metrics are exposed correctly in the explorer section.
- Refer to [grafana.testnet.penumbra.zone](https://grafana.testnet.penumbra.zone/?orgId=1) and create grafana dashboards for Penumbra fullnode.

### Validator Setup

If you want to take it to the next level and become a validator check [Validator documentation](https://guide.penumbra.zone/node/pd/validator.html).