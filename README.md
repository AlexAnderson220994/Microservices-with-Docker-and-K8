# Microservices

## Docker

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

## Kubernetes (K8)