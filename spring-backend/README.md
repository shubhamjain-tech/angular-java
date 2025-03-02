# Connect RDS-DB to backend 

Note: when u are created RDS then do this step
Go to this location spring backend app conf database url path inside backend \
( /angular-java/spring-backend/src/main/resources/application.properties  ) 

![image](https://github.com/user-attachments/assets/c417b0b8-1c35-4934-b892-2dc50b33456b)


# If you install mariadb directly on your server so do this configuration 

Go to this location for connect your db to backend
( /angular-java/spring-backend/src/main/resources/application.properties  ) 


![image](https://github.com/user-attachments/assets/19a7d086-f82a-4e36-bea7-cccb70385308)


After do above configurations u can run follwing command manually for run backend or run dockerfile to create image and run continer for creating backend.

after backend continer will be running state Hit instance public-ip:8080/api/v1/workers  (to check your backend is working or not)

 
# Installation Guide for Spring Backend Application in Ubuntu Instance

This guide provides step-by-step instructions for setting up and running a Spring backend application on Ubuntu.

## Prerequisites
- Ubuntu operating system
- Internet connection

## Instructions

1. **Update apt package index:**

    ```bash
    sudo apt update
    ```

2. **Install OpenJDK 8:**

    ```bash
    sudo apt install openjdk-8-jdk
    ```

3. **Install Maven:**

    ```bash
    sudo apt install maven
    ```

4. **Build the project using Maven:**

    ```bash
    mvn clean package -Dmaven.test.skip=true
    ```

5. **Run the application:**

    ```bash
    java -jar target/spring-backend-v1.jar
    ```

## Notes
- Make sure you have the necessary permissions to execute the commands with `sudo`.
- Ensure that you have the appropriate Java and Maven versions compatible with your Spring application.
- Adjust the file paths and application names as per your project's structure.

Feel free to modify this guide according to your specific requirements.

## Dockerfile
```dockerfile
# Use Ubuntu as base image
FROM ubuntu:latest

# Install dependencies
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk maven && \
    rm -rf /var/lib/apt/lists/*

# Set the working directory in the container
WORKDIR /app

# Copy the Maven project directory into the container
COPY . /app

# Build the Maven project
RUN mvn clean package -Dmaven.test.skip=true

# Expose the port the application runs on
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "target/spring-backend-v1.jar"]
```

Note: If you wants to run backend on Kubernetes Follow following steps
- Install kubectl on server
- Install eksctl
- Create cluster using command
- Create a Docker image using above dockerfile
- Push docker iamge on AWS-ECR
- Create a Deployment.yml file (mentioned your docker image in file)
- Create a service.yml file (user service type cluster IP or node port)
- check your backend POD working or not
- after backend pod will be running state Hit instance public ip:8080/api/v1/workers (to check your backend is working or not)

  

