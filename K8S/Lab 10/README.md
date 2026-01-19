# Lab 10: Node Isolation Using Taints in Kubernetes

## Objective

The goal of this lab is to demonstrate node isolation in Kubernetes using **taints**. A Kubernetes cluster with **two nodes** is created, one node is tainted with a specific key-value pair, and the taint is verified using node descriptions.

---

## Step 1: Start Minikube Cluster

Minikube was already running with a single node. Attempting to start Minikube with two nodes using `--nodes 2` resulted in an error because the cluster already existed.

```bash
minikube start --nodes 2
```

Minikube indicated that the number of nodes cannot be changed for an existing cluster and suggested adding a node instead.

---

<img width="1089" height="243" alt="start" src="https://github.com/user-attachments/assets/c02925be-b110-4b93-b814-a1cd00e0cf27" />


## Step 2: Add a Second Node to the Cluster

A second node was added to the existing Minikube cluster using the following command:

```bash
minikube node add
```
```bash
kubectl get nodes
```
<img width="866" height="247" alt="add-get-node" src="https://github.com/user-attachments/assets/5a16cacc-4c58-402d-823f-ffc1f2290250" />

## Step 4: Apply Taint to the Worker Node

The worker node `minikube-m02` was tainted with the following parameters:

* Key: `node`
* Value: `worker`
* Effect: `NoSchedule`

```bash
kubectl taint nodes minikube-m02 node=worker:NoSchedule
```
<img width="956" height="45" alt="taint" src="https://github.com/user-attachments/assets/d1020b56-64f4-4244-87cd-616f0b6fb20c" />



## Step 5: Verify the Taint

The taint was verified by describing the worker node:

```bash
kubectl describe node minikube-m02
```

The following taint appeared in the output:

```text
Taints: node=worker:NoSchedule
```

<img width="820" height="421" alt="describe" src="https://github.com/user-attachments/assets/865e344b-f16e-4cba-b158-ab789cc944be" />

## Step 6: Validate NoSchedule Behavior

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
<img width="793" height="38" alt="validate1" src="https://github.com/user-attachments/assets/c48d7365-7314-4f85-a308-b66b1244c53f" />
<img width="945" height="57" alt="validate2" src="https://github.com/user-attachments/assets/22accb9e-b98a-453b-bd98-7a421ff0b726" />

## Conclusion

This lab successfully demonstrated:

* Creating a multi-node Kubernetes cluster
* Isolating a node using taints
* Verifying taints using Kubernetes commands
* Observing the effect of taints on pod scheduling

---


