# django-todo
A simple todo app built with django
![todo App](https://raw.githubusercontent.com/shreys7/django-todo/develop/staticfiles/todoApp.png)

### Setup
To get this repository, run the following command inside your git enabled terminal
```bash
$  https://github.com/janvykumar/Todo-list-cicd.git
```
### Deploying the App using Docker 

Create an EC2 Instance and clone the project.
Installing Docker
```bash
$  sudo yum update -y
$  sudo yum install -y docker
$  sudo systemctl start docker
$  sudo systemctl enable docker
```
Create Docker File 
Docker file consists of commands that are used to run this project. Refer to Dockerfile in this repo.
Build the image from this docker file for this project 
```bash
$  sudo docker build . -t todo-app
```
Running the above command will execute the docker file and gives you a image, also called container id.
To run this container 
```bash
$  sudo docker run -p 8000:8000 container-id
```
(-p 8000:8000 maps the port of host machine to the port of our virtual env. Here our virtual env is docker container)
Hit server:port in the browser - app will be running
To run this app in the background 
```bash
$  sudo docker run -d -p 8000:8000 container-id
```
