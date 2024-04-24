---

layout: home
title: Building a Three-Tier Application with Docker
---
Prerequisites
Before you begin, make sure you have the following prerequisites:

Docker installed on your local machine
A Dockerhub account (you can sign up for free at Dockerhub)


In this tutorial, we'll walk through the process of building a three-tier application using Docker. A three-tier architecture consists of three distinct layers: presentation tier (frontend), application tier (backend), and data tier (database). We'll containerize each tier separately and set up a multi-container environment.

Node.js application follows a three-tier architecture:
Database Tier: Utilizing MongoDB for data storage and management.
Frontend and Backend Tier: HTML and CSS for frontend and Node.js is used for backend development.
Management Server: mongo-express serves as a web-based interface for managing the MongoDB database.


## Step by Step Process
Step 1:
Create a Docker network to ensure container isolation. This will help in managing communication between containers.

![Alt Text](img1.jpg)

Step 2: Run the Database Container
Run the MongoDB container with the following command:

![Alt Text](img3.jpg)

Step 3: Creates a detached MongoDB container
Connects it to a specified Docker network.
Maps host port 27017 to container port 27017 for MongoDB client connections.
Sets the MongoDB root username to "admin" and password to "password".
Uses the official MongoDB Docker image.
![Alt Text](img2.jpg)
![Alt Text](img3.jpg)

Step 4: Run the mongo-express Server
Run the mongo-express server container using the following command:
![Alt Text](img4.jpg)

Access the mongo-express interface by navigating to http://localhost:8081 in a web browser. You will be prompted to enter the username and password. Use the provided credentials: username - admin, password - pass.
Once logged in, you will be able to see the mongo-express dashboard.

![Alt Text](img9.jpg)
![Alt Text](img10.jpg)


Step 5: Create Docker Image for the Application
Navigate to the 'app' folder of the project and create a Dockerfile. Add the below instructions to the Dockerfile for building the Docker image for the application.

FROM node: This line specifies the base image to use for building the Docker image. In this case, it uses the official Node.js image from Docker Hub.
WORKDIR /app: This sets the working directory inside the container to /app. It means that any subsequent commands will be executed from this directory.
COPY . . : This copies the contents of the current directory (where the Dockerfile is located) into the /app directory within the container. The first . refers to the source directory (the current directory), and the second . refers to the destination directory (the /app directory inside the container).
ENV MONGO_DB_USERNAME=admin: This sets an environment variable named MONGO_DB_USERNAME with the value admin inside the container. This variable will be accessible to the application running in the container.
ENV MONGO_DB_PWD=password: Similar to the previous line, this sets an environment variable named MONGO_DB_PWD with the value password inside the container.
RUN npm install: This command install the Node.js dependencies for the application. It executes the npm install command inside the container's /app directory.
EXPOSE 3000: This instruction informs Docker that the container listens on port 3000 at runtime. However, it does not actually publish the port. It's a way to document which ports the container is designed to use.
CMD [ "node", "server.js" ]: This specifies the command to run when the container starts. It runs the Node.js application by executing node server.js. This assumes that server.js is the entry point file for the Node.js application.

![Alt Text](img5.jpg)
![Alt Text](img6.jpg)
![Alt Text](img7.jpg)

Step 6: Update server.js and Build Docker Image
Make the necessary changes to the 'server.js' file to replace occurrences of 'localhost' with the name of the MongoDB container.
![Alt Text](img8.jpg)

Step 7:Once the changes are made, build the Docker image using the provided Dockerfile and run the container with the following command:

![Alt Text](img11.jpg)
![Alt Text](img12.jpg)
![Alt Text](img13.jpg)

Step 8:Upon successful execution, you can access the website at http://localhost:3000 and interact with it.

![Alt Text](img14.jpg)



