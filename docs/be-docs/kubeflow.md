---
layout: default
title: Kubeflow
parent: Backend
nav_order: 2
---

# Kubeflow

## Introduction

Kubeflow is a platform built on top of kubernetes, designed to simpfly the deployment of machine learning workflows on Kubernetes clusters. It provides an end-to-end machine learning ecosystem, featuring tools for building, training, deploying and scaling ML models.


## Setup locally

## minikube

Minikube is local Kubernetes.

Install from image:

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64
sudo install minikube-darwin-amd64 /usr/local/bin/minikube
```

Start minikube:
```
minikube start --cpus 4 --memory 8096 --disk-size=40g
```

Deploy kubeflow template to minikube cluster:
```
export PIPELINE_VERSION=1.8.5
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
kubectl wait --for condition=established --timeout=60s crd/applications.app.k8s.io
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-pns?ref=$PIPELINE_VERSION"
```

Check pods from kubleflow namespace to see the statuses of pods:
```
kubectl get pods -n kubeflow
```

Forward the network traffic

```
kubectl port-forward -n kubeflow svc/ml-pipeline-ui 8080:80
```

The kubeflow's ui panel is available at: [http://localhost:8080/](http://localhost:8080/)
