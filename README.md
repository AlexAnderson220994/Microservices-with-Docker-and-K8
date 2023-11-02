# Microservices

## Docker

### What is Docker?

- Docker is a platform for developing, shipping, and running applications in containers. 
- Containers are lightweight, portable, and self-sufficient environments that include an application and all its dependencies (libraries, configurations, etc.). 
- Docker provides a way to package, distribute, and run applications consistently across different environments, from a developer's laptop to production servers.

### Why use Docker?

- Consistency: Ensures applications work the same everywhere.
- Isolation: Prevents conflicts between apps on the same system.
- Portability: Works on any system, making deployment easier.
- Scalability: Easily scales based on demand.
- Resource Efficiency: Efficient in terms of memory and CPU.
- Rapid Deployment: Quick start/stop for faster development.

### Setting up Docker

#### Installing Docker

- Go to the Docker website to install Docker Desktop
````
https://www.docker.com/products/docker-desktop/
````
- Choose the correct download for your OS.
- You can view your image library on the Docker Desktop console

![Alt text](<images/3. docker desktop.jpg>)

#### Make a Docker Hub account

- Sign up to Docker Hub with a personal email address.
- This is where you can make new repositories for your Docker Images.

![Alt text](<images/1. dockerhub repos.jpg>)

- Previously made images can be pulled from the repo

![Alt text](<images/2. dockerhub pull command.jpg>)

#### Using Docker

1) Open GitBash and Login to Docker.
````
docker login
````
- Input your Docker username and password if prompted.
2) Test that Docker is installed with:
````
docker
````
AND/OR
````
docker --version
````
3) Check which Docker images have been added with:
````
docker images
````
4) To see which Docker containers are running:
````
docker ps
````
5) To run a Docker container:
````
docker run -d -p 80:80 <container-name>
````
- `-d` - detached mode (runs in background)
- `-p` - the port the container runs on
- `80:80` - mapped port:port
6) To start a container running:
````
docker start <container-ID>
````
7) To stop a container running:
````
docker stop <container-ID>
````
8) To remove a container:
````
docker rm <container-ID> -f
````
9) To remove an image:
````
docker rmi <image-ID> -f
````

#### Accessing the Shell in a Docker container

1) Run the below command to bring up the list of containers:
````
docker ps
````
2) Connect to the shell for that container with:
````
docker exec -it <container-ID> sh
````
- `-it` - interactive
- Up and down commands don't work when connecting to this shell.
- If this command doesn't work, run the following command first:
````
alias docker="winpty docker"
````
3) Install any dependencies you need:
````
apt update -y
````
````
apt upgrade -y
````
````
apt install sudo
````
````
apt install nano
````
````
apt install systemctl
````
- The container is extremely lightweight so a lot of things won't be pre installed.

#### Making a Docker image

1) Make a folder on your local system for Docker.
2) Make a file in this folder called index.html
````
touch index.html
````
- Modify this file with:
````
nano index.html
````
- Make any edits you want to make to this file.
3) Make a `Dockerfile`:
````
touch Dockerfile
````
- Modify this file with:
````
nano Dockerfile
````
- Input the following
````
FROM nginx
COPY index.html /usr/share/nginx/html
````
- This uses the nginx image and copies/replaces your new local index.html file into the specified file path.
4) Build the Docker image:
````
docker build -t <image-name>
````
5) Make a repo on Docker hub for this image.
6) Tag the Docker image:
````
docker tag <image-name> <docker-hub-username/repo-name:tag>
````
7) Push the Docker image to the repo:
````
docker push <docker-hub-username/repo-name:tag>
````

#### Making a NodeJS image

1) Make a local host folder for Docker.
2) Make a Dockerfile in that folder from the GitBash terminal:
````
nano Dockerfile
````
- note Dockerfile needs a capital D
3) Put the following inside the Dockerfile:
````
# Node version
FROM node:12

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install app dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Expose the port that the app runs on
EXPOSE 3000

# Command to run the app
CMD [ "node", "app.js" ]
````
4) Build the image (make sure you're located in the folder with the Dockerfile):
````
docker build -t alexanderson2209/tech254-nodejs
````
5) Run the container:
````
docker run -d -p 3000:3000 alexanderson2209/tech254-nodejs
````
6) Go to `http://localhost:3000` to see the application running.

## Kubernetes (K8)

### K8 Architecture



### Why use K8?

- K8 is an open source orchestraction platform widely used in the world of cloud-native application development and deployment.

### Benefits of K8

- Orchestrate containers - Kubernetes automates the deployment, scaling, and management of containers.
- Scalability - Applications can be scaled horizontally, adding or removing containers when needed to handle traffic.
- Highly available - K8 can automatically distribute containers across multiple nodes, so if one node fails it can still run on a healthy node.
- Portable - K8 can be run on various cloud providers, on-prem datacentres, or hybrid environments.
- Large community - K8 is open source and has a large and active community - lots of support and documentation.
- Cost efficient - Resource usage is optimised and management tasks are automated, resulting in reduced operational costs during deployment.

### When would you not use K8?

- Simplicity - If an application is straightforward and doesn't require scaling - K8 will add unnecessary complexity.
- Limited resources - For small teams or teams with limited resources, setting up K8 clusters can be time consuming and take up a lot of resource.
- Using K8 effectively requires skilled infrastructure personnell