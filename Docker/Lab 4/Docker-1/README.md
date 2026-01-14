# Lab 4 – Run Java Spring Boot Application in Docker
## Objective
Run a Java Spring Boot application inside a Docker container using Java 17 JRE.

## Prerequisites
-Docker installed
-Git installed
-Java & Maven installed
-Linux / WSL environment

## Application Source
https://github.com/Ibrahim-Adel15/Docker-1.git

### Step 1: Clone the Application Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```
![screen](lab4-screenshot/clone)
### Step 2: Build the Application

```bash
mvn clean package
```

The generated JAR file will be created at:

target/demo-0.0.1-SNAPSHOT.jar
![screen](lab4-screenshot/build)
### Step 3: Create Dockerfile
Create a file named Dockerfile with the following content:

```bash
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
CMD ["java","-jar","app.jar"]
```

### Step 4: Build Docker Image

```bash
docker build -t app2 .
```

Check image size:

```bash
docker images app2
```

![screen](lab4-screenshot/size)
### Step 5: Run Container
```bash
docker run -d -p 8080:8080 --name container2 app2
```

![screen](lab4-screenshot/run)
### Step 6: Test the Application

Open your browser and go to:
```bash
http://localhost:8080
```

![screen](lab4-screenshot/test)

## Conclusion

The Spring Boot application was successfully built, containerized, and executed using Docker with Java 17 JRE.
