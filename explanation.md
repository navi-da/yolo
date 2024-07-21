## 1. Choice of Base Image
 The base image used to build the containers is `node:14-alpine`. It was used instead of the Node and node-slim images due to small file size 
 Used 
 1. Client:`node:14-alpine`
 2. Backend:`node:14-alpine`
 3. Mongo:`mongo:latest`
       

## 2. Dockerfile directives used in the creation and running of each container.
**Client Dockerfile**

```
# Use an official Node runtime as a parent image
FROM node:14-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Define the command to run your app
CMD ["npm", "start"]

```
**Backend Dockerfile**

```
# Use an official Node runtime as a parent image
FROM node:14-alpine

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Expose the port the app runs on
EXPOSE 5000

# Define the command to run your app
CMD ["node", "server.js"]

```

## 3. Docker Compose Networking
The (docker-compose.yml) defines the networking configuration for the project. It includes the allocation of application ports. The relevant sections are as follows:


```
services:
  yolo-backend:
    # ...
    ports:
      - "5000:5000"
    networks:
      - yolo-net

  yolo-client:
    # ...
    ports:
      - "3000:3000"
    networks:
      - yolo-net
  
  yolo-mongo:
    # ...
    ports:
      - "27017:27017"
    networks:
      - yolo-net

networks:
  yolo-net:
    name: yolo-net
    driver: bridge
    attachable: true

```
In this configuration, the backend container is mapped to port 5000 of the host, the client container is mapped to port 3000 of the host, and mongodb container is mapped to port 27017 of the host. All containers are connected to the yolo-net bridge network.


## 4.  Docker Compose Volume Definition and Usage
The Docker Compose file includes volume definitions for MongoDB data storage. The relevant section is as follows:


```
yolo-mongo:
  # ...
  volumes:
    - type: volume
      source: yolo-data
      target: /data/db

volumes:
  yolo-data:
    driver: local

```


## 5. Git Workflow to achieve the task

To achieve the task the following git workflow was used:

Fork the repository from the original repository.
Clone the repo using `git clone https://github.com/navi-da/yolo.git`
Modify the Dockerfile for the backend
`git add client/Dockerfile`
Committed the changes:
`git commit -m "Update backend Dockerfile"`
Add Dockerfile for the client
`git add backend/dockerfile`
Committed the changes:
`git commit -m "Update client Dockerfile"`
Modify docker-compose file in the repo:
`git add docker-compose.yaml`
Committed the changes:
`git commit -m "Modify docker-compose"`
Update the MONGO_URI in the backend server file 
`git add backend/server.js`
Committed the changes:
`git commit -m "Update backend server file"`
Update README.md
`git add README.md`
Committed the changes:
`git commit -m "Update README with setup instructions"`
Push changes to github:
`git push`

Built the client and backend images:
`docker build -t yolo_client:v1.0.0 . `
`docker build -t yolo_backend:v1.0.2 .`
Tag the images
`docker tag yolo_client:v1.0.0 navida/yolo_client:v1.0.0`
`docker tag yolo_backend:v1.0.2 navida/yolo_backend:v1.0.2`
Pushed the built imags to Docker Hub
`docker compose push`


