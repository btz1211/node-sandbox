## Overview
This is the API service that provides APIs for accessing apprentice related data

### Local Development
The project utilizes docker and kubernetes for deployment. Follow the instructions below for building and running application

To simply run the server, run `node server.js`

#### Docker Instructions
To run server using docker:
- build - `docker build -t apprentice-api .`
- run - `docker run -d -p 8080:8080 apprentice-api`

To build and push image to registry
- login - `ws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 957687255356.dkr.ecr.us-west-2.amazonaws.com`
- tag - `docker tag apprentice-api:latest 957687255356.dkr.ecr.us-west-2.amazonaws.com/apprentice-api:latest`
- push - `docker push 957687255356.dkr.ecr.us-west-2.amazonaws.com/apprentice-api:latest`


#### Kubectl instructions
The service uses AWS EKS. Therefore, make sure you have your local setup connecting to the right aws account. For more information on this check out this [link](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds)

- first make sure you've installed kubernetes ([kubectl setup](https://kubernetes.io/docs/setup/))
- connect to aws eks cluster by running `aws eks --region us-west-2 update-kubeconfig --name apprentice-api-dev`
- run `kubectl apply -f kube` to create the deployment + service
- run `kubectl get service` to get the `external ip`
- you can connect to the service by going to [external ip]:8080


