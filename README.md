[![CircleCI](https://circleci.com/gh/Talismanic/udacity-ml-kubernetes.svg?style=svg)](https://circleci.com/gh/Talismanic/udacity-ml-kubernetes)


## Project Summery
This is the 5th project of Udacity Nanodegree of Cloud Engineer. In this project we will build a kubernetes cluster where a machine learning model will run. An API is exposed which takes input of different property of house and predict the house price.

## Dependencies
Docker
Minikube
python3
pip
venv
## Instruction
### Step 01 : Checking python app locally
Clone the code from repository. 
```
git clone https://github.com/Talismanic/udacity-ml-kubernetes.git
```

Create a virtualenv and activate it

```
python3 -m venv ~/.devops
source ~/.devops/bin/activate   
```
Install necessary dependencies with Makefile
``` 
make install
```
Run standalone app: 
```
python app.py
```
### Step 02 : Running App in Docker 

Run the shell: 
```
./run_docker.sh
```
This will build a docker container and run it on 8000 port of host. Then open a new terminal window keeping the container window open. Then call the API with the following shell script to get the output of in the previous window:
```
./make_prediction.sh
```

### Step 03 : Running App in K8s

Run the shell
```
./run_kubernetes.sh
```
This will show the container creating status. Wait for sometime and after that in another terminal run following command to check the pod status:
```
kubectl get pods
```
Run prediction : 
```
./make_prediction_k8s.sh
```
### Step 04: Adding Circle CI
Go to CircleCi and open an account with Github as organization. The add this project with the provided configuration. The add any line in readme and push to github. This will trigger a build and you will see whether it has failed or passed.


## File Explaination
### makefile 
Instructions to setup python environment and lintins are here.
### app.py 
the main python program whic exposed the API and run the model.
### Dockerfile 
Definition of the Docker container is there which run python cmd and exposes the service in port 80/
### run_docker.sh 
Build the docker container from Docker file and runs it on hostport 8000
### make_prediction.sh 
Tests  the API exposed through docker container connecting with hostport 8000
### upload_docker.sh 
Uploads the image to dockerhub
### run_kubernates.sh 
Pulls the docker image from dockerhub and creates a deployment with that image. 
### make_prediction_kubernetes.sh 
Tests  the API exposed through kubernetes cluster connecting with hostport 8001
### docker_out.txt and kubernetes_out.txt
These two files contain the output of terminal while testing the APIs through make_prediction.sh and make_prediction_k8s.sh
### .circleci/config.yml 
This file contains circleci configuration specifying steps to lint and build the project
