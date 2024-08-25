# **Docker Cheat Sheet**

## **1. Basic Concepts**

### **1.1. Containers**
- **Description:** Containers are lightweight, standalone, and executable packages that include everything needed to run an application—code, runtime, system tools, libraries, and settings.
- **Example:**
  ```bash
  docker run hello-world
  ```

### **1.2. Images**
- **Description:** Images are read-only templates used to create containers. They include the application code, libraries, and dependencies.
- **Example:**
  ```bash
  docker pull ubuntu
  docker images
  ```

### **1.3. Dockerfile**
- **Description:** A `Dockerfile` is a script containing a series of instructions to build a Docker image. Each instruction in a Dockerfile creates a new layer in the image.

#### **Writing a Dockerfile**

1. **Base Image** - Specify the base image to use.
2. **Working Directory** - Set the working directory inside the container.
3. **Copy Files** - Copy files from the host to the container.
4. **Install Dependencies** - Install necessary packages and dependencies.
5. **Expose Ports** - Define which ports the container will listen on.
6. **Command** - Specify the command to run when the container starts.

- **Example:**
  ```dockerfile
  # Use an official Node.js runtime as a parent image
  FROM node:14

  # Set the working directory in the container
  WORKDIR /usr/src/app

  # Copy package.json and install dependencies
  COPY package*.json ./
  RUN npm install

  # Copy the rest of the application code
  COPY . .

  # Expose port 8080
  EXPOSE 8080

  # Define the command to run the app
  CMD ["node", "app.js"]
  ```

### **1.4. Docker Compose**
- **Description:** Docker Compose is a tool for defining and running multi-container Docker applications. It uses a `docker-compose.yml` file to configure application services.

#### **Writing a `docker-compose.yml` File**

1. **Version** - Specify the version of the Compose file format.
2. **Services** - Define the services (containers) that make up your application.
3. **Build** - Optionally, specify build context or Dockerfile.
4. **Ports** - Map container ports to host ports.
5. **Environment** - Set environment variables.
6. **Volumes** - Mount host directories or volumes into the container.

- **Example:**
  ```yaml
  version: '3'
  services:
    web:
      image: nginx
      ports:
        - "80:80"
    db:
      image: postgres
      environment:
        POSTGRES_DB: exampledb
        POSTGRES_USER: user
        POSTGRES_PASSWORD: password
      volumes:
        - postgres_data:/var/lib/postgresql/data
  volumes:
    postgres_data:
  ```

## **2. Advanced Concepts**

### **2.1. Volumes**
- **Description:** Volumes are used to persist data created by and used by Docker containers.
- **Example:**
  ```bash
  docker run -v /host/path:/container/path myimage
  ```

### **2.2. Networks**
- **Description:** Docker networks allow containers to communicate with each other and with the outside world.
- **Example:**
  ```bash
  docker network create my-network
  docker run --network my-network mycontainer
  ```

### **2.3. Docker Swarm**
- **Description:** Docker Swarm is Docker’s native clustering and orchestration tool for managing a cluster of Docker engines.
- **Example:**
  ```bash
  docker swarm init
  docker service create --name my-service --replicas 3 -p 80:80 nginx
  ```

### **2.4. Multi-Stage Builds**
- **Description:** Multi-stage builds allow you to use multiple `FROM` statements in a Dockerfile to optimize image size by using intermediate images.
- **Example:**
  ```dockerfile
  # First stage: build
  FROM node:14 AS builder
  WORKDIR /app
  COPY . .
  RUN npm install && npm run build

  # Second stage: production
  FROM nginx:alpine
  COPY --from=builder /app/build /usr/share/nginx/html
  ```

### **2.5. Docker Secrets**
- **Description:** Docker Secrets manage sensitive data, such as passwords and API keys, in a secure manner within Docker Swarm.
- **Example:**
  ```bash
  echo "my_secret_password" | docker secret create db_password -
  ```

## **3. Commands**

### **3.1. Basic Commands**
- **List Containers:** `docker ps`
- **List Images:** `docker images`
- **Run a Container:** `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`
- **Stop a Container:** `docker stop CONTAINER_ID`
- **Remove a Container:** `docker rm CONTAINER_ID`
- **Remove an Image:** `docker rmi IMAGE_ID`

### **3.2. Managing Docker**
- **Build an Image:** `docker build -t myimage .`
- **Tag an Image:** `docker tag IMAGE_ID myusername/myimage:tag`
- **Push an Image:** `docker push myusername/myimage:tag`
- **Inspect an Image/Container:** `docker inspect IMAGE_ID/CONTAINER_ID`
- **View Logs:** `docker logs CONTAINER_ID`
