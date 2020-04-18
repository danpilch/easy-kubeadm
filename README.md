# easy-kubernetes
Setup a Kubernetes v1.18 cluster easily on CentOS 8

## Overview

This project intends to show how easy it is to setup a K8s cluster with minimal experience using Kubnernetes. I have adapted this project from the great guide: [Installing Kubernetes on Linux with kubeadm](http://kubernetes.io/docs/getting-started-guides/kubeadm/)

This system uses CRI-O container runtime

### Requrements

Ansible (tested on 2.9.6)

CentOS (v8) hosts (be it, AWS, GCP or  DigitalOcean etc.)

Vagrant (thanks @[xenithorb](https://github.com/xenithorb))

### Installation

Setup 3 vanilla CentOS machines with your chosen provider (I'm using DigitalOcean).

1x master
3x nodes

In your [inventory](./inventories/main.ini) place the IP addresses you intend to use.

Now you can provision your K8s cluster with:

`ansible-playbook create-cluster-playbook.yml -b --user=root`

### Vagrant usage

You may need to change the brige interface in `tests/Vagrantfile` from `bridge: "wlp2s0"` to whatever is suitable for your environment.

```
cd tests
vagrant up

# copy kubeconfig to host
vagrant plugin install vagrant-scp
vagrant scp easy-kube-master:~/.kube/config ~/.kube
```
