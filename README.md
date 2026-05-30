# Jenkins-Test (Simple Spring Boot UI)

This is a minimal Spring Boot web application that serves a simple UI on http://localhost:8081.

How to run (Windows, cmd.exe):

1. Open a command prompt in the project folder `Jenkins-Test`.
2. Build and run with Maven wrapper (included):

```cmd
mvnw.cmd spring-boot:run
```

Or build a jar and run:

```cmd
mvnw.cmd package
java -jar target\Jenkins-Test-0.0.1-SNAPSHOT.jar
```

Open http://localhost:8081/ in your browser. Click the "Call API" button to call `/api/hello`.
