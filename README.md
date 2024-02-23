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
  Here the port 4000 of the VM "Eazytraining" will forward by the port 5000 of our container "test-api"

  ![container](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/6a299665-356f-4912-a0e1-e771b0b0527c)


  4- 
    Test the api through the frontend :
 Using command line :

The next command will ask the frontend container to request the backend api and show you the output back. The goal is to test both if the api works and if frontend can get the student list from it.

![list-student](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/5557d5b3-5e0a-4438-9b47-5050b56932ef)

I'm using the hostname IP "127.0.0.1" beacause i'm in localy.
my application which responds from the "student_age.json" script" giving me the list of students and their ages.

![localhost](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/463bff07-a2a4-4a0a-a5b3-ecb834217615)

**so far I'm validating the Build and Test part of my muni docker project.**

# Infrastructure As Code 
we need to set up a docker compose that will allow us to automate the deployment of our infrastructure.
The goal is to create a second "website" container with the required recommendations.

Let me remove the test container and the test network before to lauch the automatic scritp to provisonne my cinfrastructure via "Docker compose"
![docker delete](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/7fefeac3-32db-4f2f-9ee3-0a51747c9181)

![network-delete](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/3c2141b4-d3a3-4d8d-b727-072ca8ec9b6f)

let build the docker-compose file with the following comand to create the network and both containerthe website and the api :

docker-compose up -d 
![Docker-copose](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/9051e1a7-1729-44e4-b1e8-ac8f0598f6a2)

![ne](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/c4163494-e7d2-4865-a7f2-e693a3147a70)

We try to test, if we can reach our website via the port of the Eazytraining VM.
![port](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/fa183485-3786-47a2-9e9b-82b8c14cd65b)

We cannot see the list of the student because we don't fill the folow parameters "(http://<api_ip_or_name:port>/pozos/api/v1.0/get_student_ages)"

![check](https://github.com/bahalphaone/mini-projet-docker/assets/36479531/5a007514-f274-4f79-b586-6fe7bfe5f7ca)


