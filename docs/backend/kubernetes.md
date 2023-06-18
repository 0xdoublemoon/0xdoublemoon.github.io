---
layout: default
title: Kubernetes
parent: Backend
nav_order: 2
---

Kubernetes is a set of processes running on several machines. It follows master worker patterns. One node is master and left are workers.

| Master node        | Work node                 |
| ------------------ | ------------------------- |
| Config store       | Docker runtime            |
| API server         | kubelet                   |
| Controller manager | Network proxy(kube-proxy) | 
| Controllers        | Monitoring                |
| Scheduler          | Pods                      |

The processes take the responsibilities of
- (master node) handling API requests from kubectl
- (master node) scheduling pods to run on worker nodes
- running a pod on the worker node
- (worker node) monitoring and networking

**etcd** is the distributed key value database implemented based on Raft consensus mechanism that **kubernetes** uses to store configuration data, system state, and metadata. 
For example, `kubectl get xyz` command is read from etcd store. `kubectl create` will create an entry in etcd.


### etcd vs. consul, which one is better?

Since etcd is just a simple distributed kv database, consul provides additional features like healthcheck and has built-in service discovery. consul is more like a solution. 