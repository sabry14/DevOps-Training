# Lab 12: Managing Configuration and Sensitive Data with ConfigMaps and Secrets

## Objective

The objective of this lab is to demonstrate how Kubernetes manages application configuration and sensitive data using **ConfigMaps** and **Secrets**. Non-sensitive MySQL configuration values are stored in a ConfigMap, while sensitive credentials are stored securely using a Secret with Base64-encoded values.

---


## Step 1: Create a ConfigMap for MySQL Configuration

A ConfigMap was created to store non-sensitive MySQL configuration variables:

* `DB_HOST`: Hostname of the MySQL StatefulSet service
* `DB_USER`: Database user for the `ivolve` database

### ConfigMap YAML File: `mysql-configmap.yaml`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-config
  namespace: ivolve
data:
  DB_HOST: mysql.ivolve.svc.cluster.local
  DB_USER: ivolve_user
```

The ConfigMap was applied using:

```bash
kubectl apply -f mysql-configmap.yaml
```
<img width="788" height="59" alt="apply" src="https://github.com/user-attachments/assets/935d8c98-edf2-499a-9ea9-a167ec38263e" />

---

## Step 2: Base64 Encode Sensitive Values

Kubernetes Secrets require values to be **Base64-encoded**. The following sensitive values were encoded:

* `DB_PASSWORD`
* `MYSQL_ROOT_PASSWORD`

Example encoding commands:

```bash
echo -n ivolve123 | base64
echo -n root123 | base64
```
<img width="684" height="76" alt="encode" src="https://github.com/user-attachments/assets/b1666ab4-4ec6-40ab-a93a-960314556b93" />

---

## Step 3: Create a Secret for MySQL Credentials

A Secret was created to store sensitive MySQL credentials securely.

### Secret YAML File: `mysql-secret.yaml`

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: ivolve
type: Opaque
data:
  DB_PASSWORD: aXZvbHZlMTIz
  MYSQL_ROOT_PASSWORD: cm9vdDEyMw==
```

The Secret was applied using:

```bash
kubectl apply -f mysql-secret.yaml
```
<img width="759" height="57" alt="apply-secret" src="https://github.com/user-attachments/assets/2eebf821-5a15-4add-ad85-58f7cccbc742" />

---

## Step 4: Verify ConfigMap and Secret

Verify the ConfigMap:

```bash
kubectl get configmap -n ivolve
```
<img width="642" height="76" alt="get" src="https://github.com/user-attachments/assets/023cfc30-7a5f-4e67-8678-98338c1e671c" />

Verify the Secret:

```bash
kubectl get secret -n ivolve
```
<img width="611" height="61" alt="get-secret" src="https://github.com/user-attachments/assets/17d6a417-7c30-4fee-83e8-04dab2d849ce" />

---

## Conclusion

This lab successfully demonstrated:

* Creating a ConfigMap for non-sensitive configuration data
* Creating a Secret for sensitive credentials
* Using Base64 encoding for Secret values
* Verifying ConfigMaps and Secrets in Kubernetes

---
