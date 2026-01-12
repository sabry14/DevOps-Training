# Build Tools with Gradle

This repository demonstrates a complete **Gradle workflow** for building and running a Java application. The steps include cloning the source code, running unit tests, packaging the application, and running it.

---

## Step 1: Clone the Repository

Clone the source code from GitHub:

```bash
git clone https://github.com/Ibrahim-Adel15/build1.git
cd build1
```

![Step 1 Screenshot](screenshot/clone.png)

---

## Step 2: Run Unit Test

Execute the unit tests for the project:

```bash
gradle test
```

![Step 2 Screenshot](screenshot/test.png)

---

## Step 3: Package the Application

Assemble the project and create the JAR file:

```bash
gradle build
```

![Step 3 Screenshot](screenshot/build.png)

---

## Step 4: Run the Application

Execute the application:

```bash
java -jar build/libs/ivolve-app.jar
```

![Step 4 Screenshot](screenshot/run.png)
