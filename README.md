# Django-App-Deployment
Creating an efficient DevOps workflow for Django app development on EC2 with Docker and Jenkins
## Technological Resources
1) GitHub
2) AWS Free Tier Account
3) Elastic Compute Cloud (EC2) Instance : t2 micro
4) Security groups
5) Docker Image
6) Docker Containers
7) Jenkinsfile
8) Continuous Integration (CI)
9) Continuous Deployment (CD)

## Deploying Django apps to EC2 with Docker and Jenkins : A Step-by-Step Guide
## Step 1 : Managing local development environment 
Before deploying your Django app on an EC2 instance, it's important to test it locally to ensure that everything is working as expected. Here are the steps to get started:

1) Create a new folder on your local machine for your Django project.

2) Open the folder in your preferred code editor, such as VS Code.

3) Open a terminal or command prompt and navigate to your project folder.

4) Clone your Django app repository using the following command :
```
git clone https://github.com/shreys7/django-todo.git
```

5) Creating Virtual Environment
```
virtualenv -p python3.11 env
```
6) Activate the vritual environment in VS Code
``` 
env\Scripts\activate
```
7) Change directory to the app directory
  ``` 
  cd django-todo
  ```
8) Create all the migrations to run this App.
```
python manage.py makemigrations
```
9) Apply this migrated command to run the following command
``` 
python manage.py migrate
```
9) Now we need to create the superuser using the following command : 
```
python manage.py createsuperuser
```
10) We just need to start the local Server using the following command : 
```
   python manage.py runserver
```
11) Now we can access the webapp on  http://127.0.0.1:8000/todos 

## Step 2 : Creating requirement file
We will create a requirement.txt file to freeze the dependencies requried to run the application using the following command : 
```
  pip freeze > requirement.txt

```
## Step 3 : Setting up our AWS EC2 instance
   Create the ec2 instance with following details
1) Instance Name : Django-Application
2) AMI : Ubuntu 18 LTS
3) Key Pair : demo.pem
4) Security Groups : Allowing SSH at Port 22

After creating the instance make sure that it is running 

Make connection with EC2 Instance using git bash CLI with the help of key pair 

Now we are on EC2 instance

We will create a new directory named projects using the following command :
```
mkdir projects
```
"I would like to extend a sincere thank you to shreys7, who contributed his source code to this project. Your efforts have helped to make this project a success, and we are grateful for your contributions."
Clone the django todo app repo in the project directory
```
git clone https://github.com/shreys7/django-todo.git
```

Change directory and move to the django-todo directory using the following command :
```
  cd django-todo/
 ```
Add your instance's public IP to allowed host in setting.py file
```
   vi todoApp/settings.py
 ```
Find allowed host and enter your public IP or just enter '*' so that all Ip's are allowed

Now go back to terminal and Install docker on the EC2 instance 
   ```sudo apt install docker.io
   ```
