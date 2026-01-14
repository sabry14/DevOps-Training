# Lab 5 – Multi-Stage Docker Build
## Objective
The goal of this lab is to build a Java Maven application using a multi-stage Docker build in order to
reduce image size and follow Docker best practices.
## Application Source
https://github.com/Ibrahim-Adel15/Docker-1.git
## Steps
### 1. Clone the repository:

'''bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
'''

### 2. Create a multi-stage Dockerfile using Maven for build and Java runtime for execution.
### 3. Build the Docker image:
docker build -t app3 .
### 4. Run the container:
docker run -d -p 8080:8080 --name container3 app3
### 5. Test the application using a browser or curl:
http://localhost:8080
### 6. Stop and remove the container:
docker stop container3
docker rm container3
## Notes
- Multi-stage builds reduce final image size
- Maven is only used during the build stage
- The final image contains only the JAR and Java runtime
