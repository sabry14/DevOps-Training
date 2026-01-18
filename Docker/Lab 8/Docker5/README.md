# Lab 8: Custom Docker Network for Microservices

This lab demonstrates how to create and use a **custom Docker network** to enable communication between microservices (frontend and backend), and how network isolation works in Docker.

---

## 📌 Objectives

* Clone frontend and backend code
* Create Docker images for frontend and backend services
* Create a custom Docker network
* Run containers on different networks
* Verify communication between containers
* Remove the custom network

---

## 🧱 Project Structure

```
Docker5/
├── frontend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── backend/
│   ├── app.py
│   └── Dockerfile
```

---

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker5.git
cd Docker5
```

📸 *Screenshot: Repository cloned successfully*

---

## 2️⃣ Frontend Dockerfile

📁 **Path:** `frontend/Dockerfile`

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

### Build Frontend Image

```bash
cd frontend
docker build -t frontend-image .
cd ..
```

📸 *Screenshot: Frontend image built*

---

## 3️⃣ Backend Dockerfile

📁 **Path:** `backend/Dockerfile`

```dockerfile
FROM python:3.10-slim

WORKDIR /app

RUN pip install flask

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

### Build Backend Image

```bash
cd backend
docker build -t backend-image .
cd ..
```

📸 *Screenshot: Backend image built*

---

## 4️⃣ Create Custom Docker Network

```bash
docker network create ivolve-network
```

Verify:

```bash
docker network ls
```

📸 *Screenshot: ivolve-network created*

---

## 5️⃣ Run Backend Container on Custom Network

```bash
docker run -d \
  --name backend \
  --network ivolve-network \
  backend-image
```

📸 *Screenshot: Backend container running*

---

## 6️⃣ Run Frontend Container (frontend1) on Custom Network

```bash
docker run -d \
  --name frontend1 \
  --network ivolve-network \
  -p 5001:5000 \
  frontend-image
```

📸 *Screenshot: frontend1 running on ivolve-network*

---

## 7️⃣ Run Another Frontend Container (frontend2) on Default Network

```bash
docker run -d \
  --name frontend2 \
  -p 5002:5000 \
  frontend-image
```

📸 *Screenshot: frontend2 running on default network*

---

## 8️⃣ Verify Communication Between Containers

### 🔹 Method Used: HTTP Communication (curl)

Since `ping` is not available in `python:slim`, HTTP testing is used.

```bash
docker exec -it frontend1 /bin/sh
```

Inside the container:

```sh
apt update
apt install -y curl
curl http://backend:5000
```

✅ **Result:** Communication succeeds between `frontend1` and `backend`.

📸 *Screenshot: Successful curl response*

---

### ❌ Test from frontend2 (Default Network)

```bash
docker exec -it frontend2 /bin/sh
curl http://backend:5000
```

❌ **Result:** Communication fails because frontend2 is not on the custom network.

📸 *Screenshot: Failed connection from frontend2*

---

## 9️⃣ Verify Network Isolation

```bash
docker network inspect ivolve-network
```

✔ Shows:

* backend
* frontend1

❌ Does NOT show:

* frontend2

📸 *Screenshot: Network inspection output*

---





## ✅ Conclusion

* Custom Docker network allows **service name-based communication**
* Containers on the default network are **isolated**
* `python:slim` images do not include `ping`, so HTTP testing is preferred

---

