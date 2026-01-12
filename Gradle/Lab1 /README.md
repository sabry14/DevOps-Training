# Build Tools with Gradle

This repository demonstrates a complete **Gradle workflow** for building and running a Java application. The steps include cloning the source code, running unit tests, packaging the application, and running it.

---

## Step 1: Clone the Repository

Clone the source code from GitHub:

```bash
git clone https://github.com/Ibrahim-Adel15/build2.git
cd build2
```

![Step 1 Screenshot](clone.png)

---

## Step 2: Run Unit Test

Execute the unit tests for the project:

```bash
./gradlew test
```

![Step 2 Screenshot](test.png)

---

## Step 3: Package the Application

Assemble the project and create the JAR file:

```bash
./gradlew build
```

![Step 3 Screenshot](build.png)

---

## Step 4: Run the Application

Execute the application:

```bash
./gradlew run
```

![Step 4 Screenshot](run.png)
