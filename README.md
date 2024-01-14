# mini-projet-docker

Firstname : BAH

Surname : MAMADOU ALPHA

For Eazytraining's 17th DevOps Bootcamp

Period : march-april-may

Sunday the 14th, Janaury 2024

# Application

I had to deploy an application named "student_list", which is very basic and enables POZOS to show the list of some students with their age.
student_list application has two modules:
    The first module is a REST API (with basic authentication needed) who send the desire list of the student based on JSON file
    The second module is a web app written in HTML + PHP who enable end-user to get a list of student
    
 # The need

 My work was to :
    build one container for each module
    make them interact with each other
    provide a private registry
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


  

