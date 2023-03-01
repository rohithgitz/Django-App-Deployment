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

Creating Virtual Environment
```
virtualenv -p python3.11 env
```

