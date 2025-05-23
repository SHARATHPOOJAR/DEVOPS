Docker Setup, Usage, and Container Management (Ubuntu)
This guide will help you install Docker on Ubuntu, create a Dockerfile, build an image, run a container, and make modifications.

Step 1: Install Docker on Ubuntu
Update existing packages

sudo apt update

Install required dependencies

sudo apt install apt-transport-https ca-certificates curl software-properties-common

Add Docker’s official GPG key

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

Add the Docker repository

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu focal stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Update the package list again

sudo apt update

Install Docker

sudo apt install docker-ce

Verify Docker installation

docker --version

(Optional) Run Docker as non-root user

sudo usermod -aG docker $USER
Then restart your system or log out and log back in

Step 2: Create a Dockerfile
Create a new project directory

mkdir my-docker-app
cd my-docker-app

Create a Dockerfile

touch Dockerfile

Example Dockerfile content (for a simple Python app):

FROM python:3.9
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
CMD ["python", "app.py"]

Add your application files like app.py and requirements.txt into the same folder

Step 3: Build the Docker Image
Inside the project directory:

docker build -t my-python-app .

Step 4: Run the Docker Container
docker run -d -p 5000:5000 my-python-app

This runs the app and maps port 5000 inside the container to port 5000 on your local machine.

Step 5: View Running Containers
docker ps

Step 6: Modify and Rebuild the Image
Make any changes in your code or Dockerfile

Rebuild the image

docker build -t my-python-app .

Stop the old container (if running)

docker ps
docker stop <container_id>

Remove old container (optional)

docker rm <container_id>

Run the new container

docker run -d -p 5000:5000 my-python-app

Step 7: Other Useful Docker Commands
List images
docker images

Remove an image
docker rmi my-python-app

View logs
docker logs <container_id>

Enter running container shell
docker exec -it <container_id> /bin/bash

Notes
Always rebuild the image after modifying files
Tag your images properly using -t name:version
Use a .dockerignore file to avoid copying unnecessary files
References
Docker Docs: https://docs.docker.com/get-started
Ubuntu Docker Install: https://docs.docker.com/engine/install/ubuntu
