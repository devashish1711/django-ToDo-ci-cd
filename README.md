# django-todo
A simple todo app built with django

![todo App](https://raw.githubusercontent.com/shreys7/django-todo/develop/staticfiles/todoApp.png)
# Setup 
## STEP 1
To get this repository, run the following command inside your git enabled terminal
```bash
$ git clone https://github.com/devashish1711/django-ToDo-ci-cd.git
```
You will need django to be installed in you computer to run this app. Head over to https://www.djangoproject.com/download/ for the download guide

The error you're encountering occurs because the source command is not recognized in Windows PowerShell. The source command is typically used in Unix-like operating systems such as Linux and macOS to activate virtual environments.(to activate the environment)
```bash
$ .\env\Scripts\Activate.ps1
```


get into django todo file via this command

```bash
$ cd django-todo
```

make sure the django is already install in the system
```bash
$ pip install django
```
Once you have downloaded django, go to the cloned repo directory and run the following command

```bash
$ python manage.py makemigrations
```

This will create all the migrations file (database migrations) required to run this App.

Now, to apply this migrations run the following command
```bash
$ python manage.py migrate
```

One last step and then our todo App will be live. We need to create an admin user to run this App. On the terminal, type the following command and provide username, password and email for the admin user
```bash
$ python manage.py createsuperuser
```

That was pretty simple, right? Now let's make the App live. We just need to start the server now and then we can start using our simple todo App. Start the server by following command

```bash
$ python manage.py runserver
```

Once the server is hosted, head over to http://127.0.0.1:8000/todos for the App.


## STEP - 2 ()
 
For  requirement.txt file

```bash
$ pip freeze > requirements.txt
```
DO YOUR "git add ." AND "git commit" COMMAND TO PUSH

## STEP - 3 (Create an AWS EC2 instance and connect to local server)

-save the AWS KEY-PAIR to your file system

-open the comand prompt, go to the file location where you save the key-pair.pem file and type the command in your command prompt
```bash
$ ssh -i "UbuntuKeyPair-01.pem" ubuntu@ec2**************.compute-1.amazonaws.com
```
it will open the new terminal of EC2 instance

upgrade and update the instance server
```bash
$ sudo apt update && sudo apt upgrade
```

Now use command to clone all the project to your local server
```bash
$ git clone https://github.com/devashish1711/django-ToDo-ci-cd.git
```

get into django todo file via this command
```bash
$ cd django-todo
```

to install python for docker
```bash
$ sudo apt install python3-pip
```
## STEP - 4 (if you are not able to install django in your server,   error: externally-managed-environment)

step1 - Install python3-venv (if not already installed): This package provides the venv module needed to create virtual environments.

```bash
$ sudo apt install python3-venv
```
step2 - Create a Virtual Environment:
```bash
$ python3 -m venv myenv
```
step3 - Activate the Virtual Environment:
```bash
$ source myenv/bin/activate
```
step4 - Install Django within the Virtual Environment:

```bash
$ pip install django
```
not needed
step5 - Deactivate the Virtual Environment when you’re done working in it:

```bash
$ deactivate
```

# Continue with  step 3

to migrate from server to cloud
```bash
$ python3 manage.py migrate
```

Starting development server 
```bash
$ python3 manage.py runserver
```
Starting development server at http://127.0.0.1:8000/

This server is accessable from anywhere but only at port 8000
```bash
$ python3 manage.py runserver 0.0.0.0:8000
```
Starting development server at http://0.0.0.0:8000/

## STEP 5 (open AWS EC2 instance )

    1.open instace
    2.Go to Security
    3.open Security groups
    4.Edit inbound rule
        type-custom TCP , Source- Custom ,  port - 8000
    5.save changes
    now open the ip address (ex- 3.82.291.191:8001)

## Step 6 (Invalid HTTP_HOST header: '3.82.291.191:8001'. You may need to add '3.82.291.191' to ALLOWED_HOSTS)

```bash
$ vi todoApp/settings.py
```
ALLOWED_HOSTS = ["*"]

now
```bash
$ python3 manage.py runserver 0.0.0.0:8000
```

to run in backend without disrubing actual code 
```bash
$ nohup python3 manage.py runserver 0.0.0.0:8000 &
```

## STEP7(stop the application )
list of all Pid on this port(8001)
```bash
$ lsof -i:8000
```

kill the process(NOTE: change the 1306 to your PID)
```bash
$ kill -9 1306
```

# Docker Deployment model (Docker implementation)

check docker is already available, if not :
```bash
$ sudo apt install docker.io
```

create docker file
```bash
$ vi Dockerfile
```
    Copy all the command in Dockerfile:-
        FROM python:3
        RUN pip install django==3.2
        COPY . .
        RUN python3 manage.py migrate
        CMD ["python3","manage.py","runserver","0.0.0.0:8000"]


To build the docker image in todo app
```bash
$ sudo docker build . -t todo-app
```

Successfully built fc7c9a901b15(your docker will have different)

Successfully tagged todo-app:latest

Run the container id :
```bash
$ sudo docker run -p 8000:8000 <fc7c9a901b15>
```

Run the docker in background(demon background)
````bash
$ sudo docker run -d -p 8000:8000 <fc7c9a901b15>
````

check the present state of docker
```bash
$ sudo docker ps
````
# JENKINS CI/CD PIPELINE

LINK - [Install-jenkins-on-aws](https://www.trainwithshubham.com/blog/install-jenkins-on-aws)

Install Java

Update your system
````bash
$ sudo apt update
````

Install java
````
$ sudo apt install openjdk-11-jre
````

Validate Installation
````bash
$ java -version
````

# Install Jenkins

Just copy these commands and paste them onto your terminal.
````bash
$ curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings jenkins-keyring.asc > /dev/null 

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update 

sudo apt-get install jenkins
````

# Start jenkins
````bash
$   sudo systemctl enable jenkins
    
    sudo systemctl start jenkins
    
    sudo systemctl status jenkins
````

# Access Jenkins UI


````bash
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
""
````
Now copy the password and paste to the <server-ip-address:8080>
Create First Admin User -> ready to go use jenkins

This command will do all the work to install jenkins and its library-single command
````bash
$ sudo docker pull jenkins/jenkins
````

this will run demon jenkins at port 8080 at backend
````bash
$ sudo docker run -d -p 8080:8080 docker.io/jenkins/jenkins:latest
````


awesome sauce👍

Cheers and Happy Coding :)

# DEVASHISH PRAJAPAT
