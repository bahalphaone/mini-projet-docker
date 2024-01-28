# mini-projet-docker

Please find the specifications by clicking [Here](https://github.com/diranetafen/student-list)

Firstname : BAH

Surname : MAMADOU ALPHA

For Eazytraining's 17th DevOps Bootcamp

Period : march-april-may

Sunday the 14th, Janaury 2024


# THE GOAL of this Mini-Project :

the goal of this project is to embed an application in a docker container.
The project has three main parts:
1- BUILd : this involves writing a Dockerfile with the instructions given in the statement, and testing the application with a "CURL" command provided in the statement, which is supplied with identifiers. 
2- IAC : set up the automation part with the As Code infrastructure using Docker compose (this tool enables us to automatize our containerized application).

3-  Registry: In this part, we're asked to create a private Registry to store our own images.
4-  IHM of the Registry: Here we could consult our own images that we've uploaded to our private registry

Translated with DeepL.com (free version)

I had to deploy an application named "student_list", which is very basic and enables POZOS to show the list of some students with their age.
student_list application has two modules:
    The first module is a REST API (with basic authentication needed) who send the desire list of the student based on JSON file
    The second module is a web app written in HTML + PHP who enable end-user to get a list of student
    


# DESING STUDENT-LIST PROJECT

![ARCHI](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/3e4c6bd9-1927-4251-8ce5-62383871d166)


 # The Explain the architecture of POZOS application:



# My plan

First, let me introduce you the six files of this project and their role

Then, I'll show you how I built and tested the architecture to justify my choices

Third and last part will be about to provide the deployment process I suggest for this application.
The files' role

In my delivery you can find three main files : a Dockerfile, a docker-compose.yml and a docker-compose.registry.yml

    docker-compose.yml: to launch the application (API and web app)
    docker-compose.registry.yml: to launch the local registry and its frontend
    simple_api/student_age.py: contains the source code of the API in python
    simple_api/Dockerfile: to build the API image with the source code in it
    simple_api/student_age.json: contains student name with age on JSON format
    index.php: PHP  page where end-user will be connected to interact with the service to list students with their age.
# Build and test
Considering you just have cloned this repository, you have to follow those steps to get the 'student_list' application ready :

    1- Change directory and build the api container image :

 ![Capture](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/c30a41a4-dc0c-4365-b16d-dd02c3459a97)

 ![Images-Docker-images-POZO](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/af69cdbd-fbfc-4716-b72b-c81869c91826)

2- Create a bridge-type network for the two containers to be able to contact each other by their names thanks to dns functions :

![NetworkPNG](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/e7744f53-4304-4166-8748-1f0d8912df06)

 We double Ckeck if the network is create

  ![check network](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/966fcbe9-1f41-4fee-a301-4b9877518217)

  3- Move back to the root dir of the project and run the backend api container with those arguments :

  cd .. 
  docker run -d --network pozos --name test-api-pozos -v ${PWD}/student_age.json:/data/student_age.json -p 4000:5000 api-pozos:v1

  ![container](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/6a299665-356f-4912-a0e1-e771b0b0527c)


  4- 
    Test the api through the frontend :
 Using command line :

The next command will ask the frontend container to request the backend api and show you the output back. The goal is to test both if the api works and if frontend can get the student list from it.

![list-student](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/5557d5b3-5e0a-4438-9b47-5050b56932ef)

