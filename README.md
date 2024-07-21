# Overview
This project involved the containerization and deployment of a full-stack yolo application using Docker.


# Requirements
Install the docker engine here:
- [Docker](https://docs.docker.com/engine/install/) 

## How to launch the application 
### Method 1

- Create a docker-compose.yaml file and paste the contents of the docker-compose.yaml in the `https://github.com/navi-da/yolo.git` repository to it

- Launch the application using docker compose up

  `docker compose up`

### Method 2
- Clone this repository to your local machine

  `git clone https://github.com/navi-da/yolo.git`

- Navigate to the root directory of your cloned repository

  `cd yolo`

- Launch the application using the docker compose command

  `docker compose up`

## Access the application on your browser using the following URL
 `http://localhost:3000/`

## How to stop the application
- Navigate back to your terminal and press "ctrl+c" 

## How to terminate the application completely
 `docker compose down`

## The Docker images used in this application are sourced from this repository

https://hub.docker.com/repositories/navida
