# Microservices

## Docker

### Why use Docker?

### Setting up Docker

#### Installing Docker

- Go to the Docker website to install Docker Desktop
````
https://www.docker.com/products/docker-desktop/
````
- Choose the correct download for your OS.

#### Make a Docker Hub account

- Sign up to Docker Hub with a personal email address.
- This is where you can make new repositories for your Docker Images.

#### Using Docker

1) Login to Docker.
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

## Kubernetes (K8)