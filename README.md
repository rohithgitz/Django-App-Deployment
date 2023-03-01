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
10) Now we need to create the superuser using the following command : 
```
python manage.py createsuperuser
```
11) We just need to start the local Server using the following command : 
```
   python manage.py runserver
```
12) Now we can access the webapp on  http://127.0.0.1:8000/todos 

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
   ```
   sudo apt install docker.io
   ```
## Step 4 : Createa  dockerfile and run it using vim/nano editor by creating a Dockerfile 
  ```
  vi Dockerfile
  ```
Enter insert mode by pressing "i" and write the file as per the following

```
FROM python : 3
RUN pip install django==3.2


COPY . .


RUN python manage.py migrate


CMD ["python","manage.py","runserver","0.0.0.0:8001"]

```
Press esc and use :wq and enter to save the file and exit vim

Now build the docker file we created -t is the tag 
```
sudo docker build . -t todo-app
 ````
   
Now you will  get a container ID. 
```
sudo docker ps
```
Copy that container ID and run the container with the following command.
``` 
sudo docker run -p 8001:8001 e7c6d49a6f8d

```

Now go to your browser and copy your public IP and use it to check if the app is running 
 Enter your public IP:8001.
 Example : 3.98.154.166:8001
 
 
## Step 5 : Install and setup jenkins on your EC2 instance
Update your system in EC2 Terminal with the following command : 
```
   sudo apt update
   ```
Install java
```
   sudo apt install openjdk-11-jre
   ```
Install jenkins : Copy these commands
                  paste them 
                  run them
                  one by one 
                  in your terminal
```
   curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
 ```
Update OS and install Jenkins : 
 ```
   sudo apt-get update
   sudo apt-get install jenkins
   ```
Start Jenkins with these commands :
```
   sudo systemctl enable jenkins
   sudo systemctl start jenkins
   sudo systemctl status jenkins
   ```
Add port 8080 to your inbound rules in secuirity groups to allow traffic on it like we did for port 8001.

Now open Jenkins in browser by using public IP and port number



Get the password from given location 
```
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
 ```


Click install suggested plugin and go ahead ith the installation

Create and setup your admin user and your are done.

You must be on the Jenkins homepage now

Open your terminal and add jenkins to sudoers so that when we build our job in jenkins it can have sudo access
   ```
   sudo visudo
   ```
use above command to open the file and then add jenkins like this

## Step 6 : Create a GitHub repo for this project and push code from local to created repository

Create a new GitHub repository

Copy the repository url, now go back to instance terminal and change the remote repository to your new repository
```
   git remote set-url origin https://github.com/amitgitz/jenkins-Deployment-projects.git
   ```
Add ll files to staged
```
   git add .
   ```

Commit all the files
```
   git commit -m "added server code "
   ```
Push the code to repository
```
   git push origin develop
   ```
## Step 7 : Integrate jenkins with GitHub
Open your instance's jenkins and go to manage jenkins > configure sytsem > find github servers here and add your github credentials and save it.

## Step 8 : Deploy the app using Jenkins 

Create a new job as a freestyle project named todo-app

Then in source code management choose git. 
And paste your repositpory url here.

And in branches to build, write develop as we have pushed our code to the develop branch.

Now in build step. Add build step as eecute shell and write the following commands.
```
   sudo docker build . -t todo-app
   sudo docker run -p 8001:8001 -d todo-app
```

Save it and click on build now to run the job.

## Step 9 : Build is succesfull
   Now we need to check the weburl at 8000 port
## Bravo! Your Web App is officially up and running.  
  
In conclusion, we have successfully created an efficient DevOps workflow for Django app development on EC2 with Docker and Jenkins. We started with testing our Django app locally and then proceeded to deploy it on an EC2 instance. We also created a Dockerfile and ran it on the instance, and finally, we installed and set up Jenkins for continuous integration and continuous deployment. This step-by-step guide should be helpful to deploy Django apps on EC2 instances with ease.  

# Thank you for reading. I hope you find it useful and informative.



