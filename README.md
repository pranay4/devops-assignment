# devops-assignment

Pre-requisites:
- As part of this assignment, I have used my local machine and did local builds.
- Used my docker hub repository for storing images that are built.
- Initiated docker swarm and performed all tasks on manager node.
- You could join worker nodes using ## docker swarm join command which creates worker node and load can be split   amongest them.

## changes to python files:

- Since we are calling the auth app from the web app, the url has to be updated as below:
    ### result = requests.post('http://auth:5001/auth', data=data).text

## Dockerfile:
- The Dockerfile for both app and web are named respectively.
- Performed local build using docker build -- shown below.


- Once the build is done, pushed the images to my private repository 
    docker push pranay504/python-webapi
    docker push pranay504/python-authapi

- I have used Docker Swarm for Orchestration - I can implement the same in Kubernetes if need be.. Please let me know.
- I have used Docker stack to deploy both the stacks together and therefore both stacks were able to communicate with each other.

## Below are the different commands I have used :

 To deploy the stack:
  docker stack deploy -c web-auth.yml web-auth 
 
 To view the stack:
 docker stack ps web-auth 
 
 To increase/decrease the replica count:
 docker service scale web-auth_web=2
 p.s: you could also mention this in the docker compose file as well.

 To check the logs: 
 docker service logs d3bnylsq0lp0

 To destroy the stack:
 docker stack rm web-auth

Steps to Production:

- Once tested in Dev & UAT- 
    - We can deploy this prod by doing some customizations like for instance we can use a second docker compose file with production specific configs and name it something like prod.yml which can be run along with the base compose file.
    - we can set the prod specific env variables.
    - change the restart policy if needed.
    - perform rolling updates.