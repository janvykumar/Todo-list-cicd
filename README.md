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

Hit serverIP:port in the browser - app will be running.

To run this app in the background 
```bash
$  sudo docker run -d -p 8000:8000 container-id
```
### Deploying the App using CI/CD Pipeline

Let's install Jenkins first. Here we will be installing Jenkins using Docker.
```bash
$ Make sure docker is installed in your system
$ Build jenkins using docker : sudo docker pull jenkins/jenkins
$ Run jenkins : sudo docker run -d -p 8080:8080 docker.io/jenkins/jenkins:latest
```
Jenkins runs on port 8080. You will need to add an inbound rule custom TCP on post 8080 from anywhere for the instance.
Hit instance-ip-address:8080 in the browser. You will be seeing Jenkins login page.Let's set this up.
To setup Jenkins, follow the below steps:
```bash
Get the password from : sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Install the suggested plugins
Once the plugins are installed, create your admin user.
```
Jenkins is ready!

Let's integrate GitHub with Jenkins

Creating Personal Access token : Go to your GitHub --> settings --> developer settings --> personal Access token --> create and save your token as you will need it in many places.
Login to jenkins using the credentials created above.
Make sure you have 'git server' plugin available. If not, install it via manage jenkins --> plugins
Configuration
```bash
manage jenkins --> system configuration --> GitHub --> Add GitHub server --> Name:GitHub, Add credentials - 'kind' should be 'secret text' - Add the personal Access Token - give 'id' as 'jenkins-github-cicd'(could be any id) --> Add
```
In the credentials dropdown, select 'jenkins-github-cicd'. you can test your connection here,it should be successful.
Save it.
We have integrated Jenkins with GitHub. Let's start with creating CI/CD Pipeline!

In Jenkins Dashboard --> create a job --> freestyle project (Todo-app) --> Ok 
configure :
```bash
source code management --> Git --> give the repo url --> We need not add the credentials here as we have already added it while integrating Jenkins and GitHub. 
Branches to build --> develop(as we are using develop branch here)
Add build step --> execute shell
shell commands :
sudo docker build . -t todo-app
sudo  docker run -p 8000:8000 -d todo-app
save
```

Build the job. Your App is up and Running now!!










