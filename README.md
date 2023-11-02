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

![Alt text](<images/4. k8 architecture.jpg>)

### What is K8?

- K8 is an open source orchestraction platform widely used in the world of cloud-native application development and deployment.
- Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

### Why use K8

- Allows you to run multiple Virtual Machines (VMs) on a single physical server's CPU. 
- Virtualisation allows applications to be isolated between VMs and provides a level of security as the information of one application cannot be freely accessed by another application.
- Open source
- Brings together development and operations by design

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
- Using K8 effectively requires skilled infrastructure personnel

### Setting up K8

#### Installing K8

1) Open the Docker Desktop window.
2) Click on the settings button.
![Alt text](<images/5. settings.jpg>)
3) On the left hand pane, click on Kubernetes.
![Alt text](<images/6. settings - k8.jpg>)
4) Tick the enable box.
![Alt text](<images/7. k8 settings.jpg>)
5) Click `Apply & restart`

#### Creating and seeing Kubernetes resources

1) To create a resource, first you need to make a Yaml file to define the resource (see next section for example).
2) Run the following command to create the resource from the Yaml file:
````
kubectl create -f <file.yml>
````
3) To view the pods that have been created:
````
kubectl get pods
````
![Alt text](<images/8. pods.jpg>)
4) To deleted a pod:
````
kubectl delete pod <pod-name>
````
5) After this a service file has to be made.
- The Kubernetes Service file is used to define and configure a Kubernetes Service, which is a fundamental resource in Kubernetes for exposing and load balancing your application within the cluster.

#### Creating nginx-deploy.yml

1) Create a Yaml file called nginx-deploy.
2) Add the following code (be careful of spacings and indentation):
````
apiVersion: apps/v1 # which API to use for deployment
kind: Deployment # pod - what kind of service/object
# What would you like to call it
metadata:
  name: nginx-deployment # name the deployment
spec:
  selector:
    matchLabels:
      app: nginx # look for this label to match with k8 service
  replicas: 3 #number of pods
  template:
    metadata:
      labels:
        app: nginx # this label connects to the service or any other k8 components
    spec:
      containers:
      - name: nginx
        image: alexanderson2209/tech254-alex-nginx:v1 # use the image on docker hub
        ports:
        - containerPort: 80
````

#### Creating nginx-service.yml

1) Make a Yaml file called nginx-service.yml
2) Add the following code (be careful of spacings and indentation):
````
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx  # This should match the labels in your Nginx deployment
  ports:
    - protocol: TCP
      port: 80  # Port to expose on the service
      targetPort: 80  # Port that the Nginx pods are listening on
  type: NodePort  # Change to LoadBalancer or ClusterIP if needed
````
- Service Type: The type field in the Service configuration specifies how the service should be exposed. Common service types include:
- ClusterIP: The service is exposed internally within the cluster.
- NodePort: The service is exposed on a specific port on each node in the cluster.
- LoadBalancer: The service is exposed using a cloud provider's load balancer.
- ExternalName: Maps the service to an external DNS name.
3) Once this has been created, the `kubectl get svc` command will show what port this is running on.
![Alt text](<images/9. nginx running.jpg>)
4) To delete a service:
````
kubectl delete service <service-name>
````
OR
````
kubectl delete -f my-service.yaml
````