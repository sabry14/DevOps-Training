# Lab 11: Namespace Management and Resource Quota Enforcement

## Objective

The purpose of this lab is to demonstrate how to manage Kubernetes namespaces and enforce resource usage limits using **ResourceQuota**. A namespace is created and a quota is applied to restrict the number of pods that can run within that namespace.

---

## Step 1: Create a Namespace

A new namespace named `ivolve` was created using the following command:

```bash
kubectl create namespace ivolve
```

The namespace creation was verified using:

```bash
kubectl get namespaces
```
<img width="732" height="172" alt="create-ns" src="https://github.com/user-attachments/assets/3c8c0a53-a91d-47ac-b108-1157253aea98" />

---

## Step 2: Create a ResourceQuota Definition

A ResourceQuota configuration file was created to limit the number of pods in the `ivolve` namespace.

File name: `pod-quota.yaml`

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: pod-limit
  namespace: ivolve
spec:
  hard:
    pods: "2"
```

The ResourceQuota was applied to the `ivolve` namespace using:

```bash
kubectl apply -f pod-quota.yaml
```
<img width="736" height="39" alt="apply" src="https://github.com/user-attachments/assets/a32dc2b6-d44b-4e67-82e4-93fefba87384" />

---

## Step 4: Verify the ResourceQuota

The applied quota was verified using:

```bash
kubectl get resourcequota -n ivolve
```
<img width="800" height="66" alt="verify" src="https://github.com/user-attachments/assets/773c5f1d-c2e7-4dd1-9c33-6dde66674499" />


The output confirmed that the maximum allowed number of pods is set to 2.

---

## Step 5: Test ResourceQuota Enforcement

### Create the first pod

```bash
kubectl run pod1 --image=nginx -n ivolve
```

### Create the second pod

```bash
kubectl run pod2 --image=nginx -n ivolve
```

A third pod was created to test quota enforcement:

```bash
kubectl run pod3 --image=nginx -n ivolve
```
<img width="1195" height="195" alt="test" src="https://github.com/user-attachments/assets/3c013f07-c6f0-4a59-98f2-6c8ba60ea8ec" />

The request was denied with an error indicating that the pod quota had been exceeded, confirming that the ResourceQuota is enforced correctly.

---

## Conclusion

This lab successfully demonstrated:

* Creating and managing Kubernetes namespaces
* Applying ResourceQuota to a namespace
* Limiting the number of pods within a namespace
* Verifying quota enforcement behavior

---
