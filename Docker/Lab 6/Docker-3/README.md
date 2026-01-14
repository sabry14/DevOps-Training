# Lab 6: Managing Docker Environment Variables (Build & Runtime)

## Objectives
### This lab demonstrates how to manage Docker environment variables using three different approaches:
-Command-line variables at runtime
-Environment variables from a file
-Environment variables defined inside the Dockerfile

### The application is a simple Flask app that displays the values of APP_MODE and APP_REGION.

## Application Overview
Language: Python
Framework: Flask
Port: 8080
Environment Variables:
APP_MODE
APP_REGION

## Project Structure
Docker-3/
│── app.py
│── Dockerfile
│── staging.env
│── README.md

### Step 1: Clone the Repository
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3

### Step 2: Dockerfile

The Dockerfile:

Uses a Python base image

Installs Flask

Exposes port 8080

Runs app.py

Sets default environment variables for production

FROM python:3.11-slim

WORKDIR /app

RUN pip install flask

COPY app.py .

ENV APP_MODE=production
ENV APP_REGION=canada-west

EXPOSE 8080

CMD ["python", "app.py"]

### Step 3: Build Docker Image
docker build -t flask-env-app .


Verify:

docker images

### Step 4: Run Containers with Different Environment Variable Methods
Case 1: Environment Variables via Command Line

(development, us-east)

docker run -d \
  -p 8081:8080 \
  -e APP_MODE=development \
  -e APP_REGION=us-east \
  --name flask-dev \
  flask-env-app


Test:

curl localhost:8081

Case 2: Environment Variables via File

(staging, us-west)

Create staging.env:

APP_MODE=staging
APP_REGION=us-west


Run container:

docker run -d \
  -p 8082:8080 \
  --env-file staging.env \
  --name flask-staging \
  flask-env-app


Test:

curl localhost:8082

Case 3: Environment Variables from Dockerfile

(production, canada-west)

No variables are passed at runtime because they are already defined in the Dockerfile.

docker run -d \
  -p 8083:8080 \
  --name flask-prod \
  flask-env-app


Test:

curl localhost:8083


## Lab Outcome:

-Built a Dockerized Flask application
-Managed environment variables using three different methods
-Ran multiple containers from the same image with different configurations
