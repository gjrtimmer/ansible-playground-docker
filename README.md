# Ansible Playground (Docker)

This is a docker based playground for Ansible. This repository provides multiple docker containers with which you will be able to play around with Ansible.

- [Quickstart](#quickstart)
- [Requirements](#requirements)
  - [docker-compose](#docker-compose)
  - [sshpass](#sshpass)
  - [Ansible Hosts File](#ansible-hosts-file)
- [Network](#network)

## Quickstart

To start the playground clone the repository, and in the repository start the containers with the command below this will start the containers in the background.

```shell
docker compose up -d
```

## Requirements

- docker / docker-desktop
- [docker compose](#docker-compose)
- [sshpass](#sshpass)

### docker-compose

Docker compose is shipped with any recent version of docker. However, when using this playground on NAS devices like QNAP or Synology, you might run into the issue that the docker version is outdated. In this case you might want to replace the `docker compose` command within this README with `docker-compose` which might be shipped with older versions of docker.

### sshpass

`sshpass` is required to be installed on your host. If you are using the recommended [Ansible Template](https://github.com/gjrtimmer/ansible-template), this will already be installed in the devcontainer.

### Ansible Hosts File

```yaml
nodes:
  vars:
    ansible_connection: ssh
    ansible_ssh_common_args: "-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
    ansible_host: localhost
    ansible_user: ubuntu
    ansible_ssh_pass: ubuntu
  hosts:
    ansible1:
      ansible_port: 2021
    ansible2:
      ansible_port: 2022
    ansible3:
      ansible_port: 2023
```

## Network

To ensure compatibility over multiple operating systems, this playground binds the various containers to the docker host. This is due to the fact that only on Linux the containers can be reached directly on their bridge network. On MacOS and Windows the container can be reached by mapping the ports, due to this reason this approach has been choosen for all operating systems.

The SSH daemon for each host is mapped to a different local port.

| Container | SSH Port |
| --------- | -------- |
| ansible1  | 2021     |
| ansible2  | 2022     |
| ansible3  | 2023     |
