# Devops


Reactjs+Docker+Jenkins+AWS Ec2:


# Docker->
Docker:
   1) Install DockerCLI in your Local system and check Docker Running Status
   2) Add Dockerfile in your project Root Directory
   3) For Docker Build : docker build . -t imageName
   4) To Run Docker : docker run <imageName>
   5) open new Terminal and run to view list of Docker image ids : docker ps
   6) To run dockerimage with Docker ID : docker exec -it DockerId
  
Sample Dockerfile:
 
![Screenshot from 2023-04-11 09-18-07](https://user-images.githubusercontent.com/89519757/231051220-33e61359-91ee-4970-b07c-c949d62c0479.png)

 # React app with Jenkins and Docker
  
 To use Travis CI just create .travis.yml :
  1) touch .travis.yml
  
  ![image](https://user-images.githubusercontent.com/89519757/231173660-8408a7fa-24d4-4df6-953f-24d6e27884b9.png)

   
 # To run Jenkins using official image from docker hub
   
   
 1) docker run --name jenkins -p 8080:8080 jenkins
 2) docker run -p 8080:8080 -v $PWD/jenkins:/var/jenkins_home jenkins
   
 
 
