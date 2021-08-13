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

<img width="1440" alt="Screen Shot 2021-08-13 at 01 01 22" src="https://user-images.githubusercontent.com/17344044/129311812-d3c34702-e2a8-42e0-9714-81360b00303b.png">
<img width="1434" alt="Screen Shot 2021-08-13 at 01 02 31" src="https://user-images.githubusercontent.com/17344044/129311816-ec35874f-3c2f-4d87-8a8a-3b035b55ccf8.png">

- Once the build is done, pushed the images to my private repository:
    
    docker push pranay504/python-webapi
    
    docker push pranay504/python-authapi

- I have used Docker Swarm for Orchestration - I can implement the same in Kubernetes if need be.. Please let me know.
- I have used Docker stack to deploy both the stacks together and therefore both stacks were able to communicate with each other.

## Below are the different commands I have used :

 To deploy the stack:
  docker stack deploy -c web-auth.yml web-auth 
  
  <img width="1026" alt="Screen Shot 2021-08-13 at 01 22 24" src="https://user-images.githubusercontent.com/17344044/129311881-8d9d3704-8e29-48e5-a746-0feae675070e.png">

 
 To view the stack:
 docker stack ps web-auth 
 
 To increase/decrease the replica count:
 docker service scale web-auth_web=2
 p.s: you could also mention this in the docker compose file as well.
 
 <img width="1025" alt="Screen Shot 2021-08-13 at 01 24 53" src="https://user-images.githubusercontent.com/17344044/129311916-f143c6b6-b293-4c1f-a8a7-ec8d03256a2b.png">

<img width="1022" alt="Screen Shot 2021-08-13 at 01 31 10" src="https://user-images.githubusercontent.com/17344044/129311934-be9b0ca1-e49d-42b6-a422-346855f8ea80.png">

 To check the logs: 
 docker service logs d3bnylsq0lp0

<img width="1027" alt="Screen Shot 2021-08-13 at 01 26 55" src="https://user-images.githubusercontent.com/17344044/129311965-3dfe925a-0552-40f0-917a-c2482288261c.png">

 To destroy the stack:
 docker stack rm web-auth

Steps to Production:

- Once tested in Dev & UAT- 
    - We can deploy this prod by doing some customizations like for instance we can use a second docker compose file with production specific configs and name it something like prod.yml which can be run along with the base compose file.
    - we can set the prod specific env variables.
    - change the restart policy if needed.
    - perform rolling updates.
