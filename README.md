# easy-kube
Setup a Kubernetes v1.4 cluster easily on CentOS 7

## Overview

This project intends to show how easy it is to setup a v1.4 K8s cluster with minimal experience using Kubnernetes. I have adapted this project from the great guide: [Installing Kubernetes on Linux with kubeadm](http://kubernetes.io/docs/getting-started-guides/kubeadm/)

### Requrements

Ansible (tested on 2.1.2.0)

CentOS (v7) hosts (be it, AWS, GCP or  DigitalOcean etc.)

Vagrant (thanks @[xenithorb](https://github.com/xenithorb))

### Installation

Setup 3 vanilla CentOS machines with your chosen provider (I'm using DigitalOcean).

1x master
2x nodes

In your [inventory](./inventories/main.ini) place the IP addresses you intend to use.

Now you can provision your K8s cluster with:

`ansible-playbook create-cluster-playbook.yml -b --user=root`

### Verification

To check if everything has provisioned correctly, on your master node, invoke:

`kubectl get nodes`

This will output all the nodes connected in the cluster:

```
NAME                 STATUS    AGE
centos-2gb-lon1-01   Ready     24m
centos-2gb-lon1-02   Ready     24m
centos-2gb-lon1-03   Ready     25m
```

To check the pod network is running correctly, invoke:

`kubectl get pods --all-namespaces`

You should see:

```
NAMESPACE     NAME                                         READY     STATUS    RESTARTS   AGE
kube-system   etcd-centos-2gb-lon1-03                      1/1       Running   0          27m
kube-system   kube-apiserver-centos-2gb-lon1-03            1/1       Running   0          28m
kube-system   kube-controller-manager-centos-2gb-lon1-03   1/1       Running   0          27m
kube-system   kube-discovery-982812725-ark01               1/1       Running   0          27m
kube-system   kube-dns-2247936740-s4zgc                    3/3       Running   0          27m
kube-system   kube-proxy-amd64-26tjw                       1/1       Running   0          27m
kube-system   kube-proxy-amd64-3n8dn                       1/1       Running   0          27m
kube-system   kube-proxy-amd64-kh8lo                       1/1       Running   0          27m
kube-system   kube-scheduler-centos-2gb-lon1-03            1/1       Running   0          26m
kube-system   weave-net-25wpd                              2/2       Running   0          27m
kube-system   weave-net-akgjx                              2/2       Running   0          27m
kube-system   weave-net-fc4or                              2/2       Running   0          27m
```
