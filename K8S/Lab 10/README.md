# Lab 10: Node Isolation Using Taints in Kubernetes

## Objective

The goal of this lab is to demonstrate node isolation in Kubernetes using **taints**. A Kubernetes cluster with **two nodes** is created, one node is tainted with a specific key-value pair, and the taint is verified using node descriptions.

---

## Environment

* OS: Ubuntu 24.04
* Kubernetes: v1.34.0
* Minikube: v1.37.0
* Driver: Docker

---

## Step 1: Start Minikube Cluster

Minikube was already running with a single node. Attempting to start Minikube with two nodes using `--nodes 2` resulted in an error because the cluster already existed.

```bash
minikube start --nodes 2
```

Minikube indicated that the number of nodes cannot be changed for an existing cluster and suggested adding a node instead.

---

## Step 2: Add a Second Node to the Cluster

A second node was added to the existing Minikube cluster using the following command:

```bash
minikube node add
```

---

## Step 3: Verify Cluster Nodes

The cluster nodes were verified using:

```bash
kubectl get nodes
```

The output confirmed that the cluster now consists of two nodes:

* `minikube` (control-plane)
* `minikube-m02` (worker node)

---

## Step 4: Apply Taint to the Worker Node

The worker node `minikube-m02` was tainted with the following parameters:

* Key: `node`
* Value: `worker`
* Effect: `NoSchedule`

```bash
kubectl taint nodes minikube-m02 node=worker:NoSchedule
```

---

## Step 5: Verify the Taint

The taint was verified by describing the worker node:

```bash
kubectl describe node minikube-m02
```

The following taint appeared in the output:

```text
Taints: node=worker:NoSchedule
```

---

## Step 6 (Optional): Validate NoSchedule Behavior

A test pod was created without any tolerations:

```bash
kubectl run nginx-test --image=nginx
```

The pod scheduling details were checked using:

```bash
kubectl get pods -o wide
```

The pod was scheduled on the control-plane node and not on the tainted worker node, confirming that the `NoSchedule` effect was enforced.

---

## Conclusion

This lab successfully demonstrated:

* Creating a multi-node Kubernetes cluster
* Isolating a node using taints
* Verifying taints using Kubernetes commands
* Observing the effect of taints on pod scheduling

---
