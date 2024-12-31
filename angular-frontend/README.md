# For angular-frontend u can create Continer using below dockerfile, or u can run below commands to build artifact and after u run all commands u can get dist folder u can move that folder into s3 bucket and using static websitehosting steps, u can run frontend. 

see the dist folder in Image
![image](https://github.com/user-attachments/assets/7a4cdcaf-8f74-4a60-a622-6bf7074df1bb)


# Before run docker file or create a artifact for code, Do follwing steps tp connect frontend to backend
Go to this location add your ec2 public-ip:8080/api/v1/workers url inside frontend/
( /angular-java/angular-frontend/src/app/services/worker.service.ts ) 

![image](https://github.com/user-attachments/assets/968b0c62-cc37-46c2-bef2-7236f0d5c36a)




# Angular Project Setup Guide

This guide provides step-by-step instructions for setting up an Angular project from scratch on an Ubuntu machine.

## Step 1: Install Node.js and npm

```bash
sudo apt update
sudo apt install nodejs npm
```
## Step 2: Check Node.js and npm versions

```bash
node -v
npm -v
```
## Step 3: Install Angular CLI globally
```bash
sudo npm install -g @angular/cli@14.2.1
```
## Step 4: Verify Angular CLI installation
```bash
ng --version
```
## Step 5: Install project dependencies (if needed)

```bash
npm install
ng build 
cd dist/angular-frontend
ng serve --host 0.0.0.0 --port=80
```
## Step 5: Deploy the artifact
Transfer the contents of the dist/ directory to your server or hosting provider to make your Angular application available to users.


# Angular Project Dockerization Guide

This guide provides step-by-step instructions for Dockerizing an existing Angular project. Docker allows you to package your Angular application into a container, making it portable and easily deployable across different environments.

## Prerequisites

- Docker installed on your system. You can download and install Docker Desktop from [here](https://docs.docker.com/engine/install/).

## Dockerfile Setup

Create a `Dockerfile` in the root directory of your Angular project with the following content:

```Dockerfile
# Use official Node.js image as the base image
FROM node:14-alpine as build

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json (if available)
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the Angular application
RUN npm run build 

# Use NGINX as the production server
FROM nginx:alpine

# Copy the built artifact from the previous stage to NGINX web server directory
COPY --from=build /usr/src/app/dist/angular-frontend /usr/share/nginx/html

# Expose port 80 to the outside world
EXPOSE 80

# Start NGINX server when the container starts
CMD ["nginx", "-g", "daemon off;"]
```

