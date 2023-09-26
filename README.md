# Docker Application Setup Guide

This guide will help you set up a Dockerized application using Docker Compose. We'll walk you through the process step by step.

Docker Document: https://docs.docker.com/language/python/
Docker Example: `git clone https://github.com/docker/python-docker`

## Prerequisites
Before you begin, make sure you have Docker Desktop and Python 3.11 installed on your system.

### 1. Create Application Folders
Create separate folders for each of your applications. For example, 'app_1' and 'app_2'.
You can refer to the sample docker application by: `git clone https://github.com/docker/python-docker`

### 2. Initialize Docker Configuration
Navigate to the app's directory:
```bash
cd app_1
```
Run the following command to initialize Docker configuration:
```bash
docker init
```
Docker Init CLI will prompt you to configure your Docker setup. Provide the requested information about your project, such as the application platform, Python version, and port number.

Once configured, Docker will create the necessary files: `.dockerignore`, `Dockerfile`, and `compose.yaml`.

Refer to the following example to answer the prompts from `docker init`.
```bash
$ docker init
Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml

Let's get started!

? What application platform does your project use? Python
? What version of Python do you want to use? 3.11.4
? What port do you want your app to listen on? 5000
? What is the command to run your app? python3 -m flask run --host=0.0.0.0
```

**Note**: Ensure you have a `requirements.txt` file in your project directory with your application's dependencies before proceeding.

### 3. Create a Virtual Environment
Create a virtual environment for each of your app using Python's built-in `venv` module:
```bash
python3 -m venv .venv
```
Activate the virtual environment:
```bash
source .venv/bin/activate
```

### 4. Create App Files
Create the main application file `app.py` and a `requirements.txt` file for this app. Add your application code and dependencies to these files.

### 5. Install Dependencies
Install the app's dependencies using pip:
```bash
pip install -r requirements.txt
```

### 6. Build Docker Image
Build a Docker image for your app:
```bash
docker build -t flask-app-1 .
```

### 7. Run Docker Container
Use the `compose.yaml` file to run the Docker container:
- Configure the `compose.yaml` file, specifying the port number if needed.
- Run the container using Docker Compose:
```bash
docker compose up --build
```

Your application will be accessible at `http://localhost:5000` with specific port you set up (i.e. 8001:5000).

### 8. Manage Docker Images and Containers
Here are some useful Docker commands for managing your images and containers:

- List all Docker images:
```bash
docker images
```

- Remove a Docker image:
```bash
docker rmi flask-app-1
```

- Tag a Docker image:
```bash
docker tag flask-app-1:latest flask-app-1:v1
```

- Check all running containers:
```bash
docker ps -a
```

- Remove a container:
```bash
docker rm <container_name>
```

- Stop containers defined in `compose.yaml`:
```bash
docker compose down
```

### 9. Run Multiple Apps Concurrently
To run multiple apps concurrently, create a global `compose.yaml` file in the root directory. In the global `compose.yaml` file, configure server name (app1/app2 ...etc) and its port number (9001:5000 ...etc), and use the following command:
```bash
cd path/to/root
docker compose up --build
```

That's it! You've successfully set up and Dockerized your application. Repeat these steps for any additional applications you want to containerize.