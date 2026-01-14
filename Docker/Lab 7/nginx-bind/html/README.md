# Lab 7: Docker Volume and Bind Mount with Nginx

This lab demonstrates the difference between Docker Volumes and Bind Mounts using an Nginx container.

## Objectives:
-Persist Nginx logs using a Docker volume
-Serve custom HTML content using a bind mount
-Verify live file updates without restarting the container

## Steps
### 1. Create Docker Volume
docker volume create nginx_logs

### 2. Create Bind Mount Directory and HTML File
mkdir -p nginx-bind/html


index.html:

Hello from Bind Mount

### 3. Run Nginx Container
docker run -d \
  --name nginx-lab7 \
  -p 8080:80 \
  -v nginx_logs:/var/log/nginx \
  -v $(pwd)/nginx-bind/html:/usr/share/nginx/html \
  nginx

### 4. Verify Nginx Page
curl localhost:8080

### 5. Modify HTML File and Verify Live Update
nano nginx-bind/html/index.html
curl localhost:8080

### 6. Verify Logs Persistence
sudo ls /var/lib/docker/volumes/nginx_logs/_data

## Notes:
-Bind Mount reflects file changes instantly
-Docker Volume persists data independent of container lifecycle
-Volumes are stored in Docker’s default volume path
