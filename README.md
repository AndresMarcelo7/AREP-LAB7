# AREP-LAB7 Safe distributed application on all fronts

Demo video is at the end of this file  

## Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.
### Prerequisites

The things you need in order to run this proyect on your computer are:
- Maven
- Git  
- Java
- Docker

Make sure you have this installed with the commands
```
mvn --version
```
```
git --version
```
```
java -showversion
```
and 
```
docker --version
```
### Documentation:
The Documentation in each Server can be generated with 
```
mvn javadoc:javadoc
```
Also in the apidocs directory you'll find the javadoc static sources.
### Install and Run
Due to the connections are made between 2 EC2 Machines wich are currently off, theres no sense to download and run the servers, but the code is available for study.
### Repositories
##### Login server:
You can see the Project Code [HERE](https://github.com/AndresMarcelo7/AREP-LAB7-LoginServer)  
CircleCI : [![CircleCI](https://circleci.com/gh/AndresMarcelo7/AREP-LAB7-LoginServer.svg?style=svg)](https://circleci.com/gh/AndresMarcelo7/AREP-LAB7-LoginServer)
##### Service Server:
You can see the Project Code [HERE](https://github.com/AndresMarcelo7/AREP-LAB7-ServiceServer)  
CircleCI : [![CircleCI](https://circleci.com/gh/AndresMarcelo7/AREP-LAB7-ServiceServer.svg?style=svg)](https://circleci.com/gh/AndresMarcelo7/AREP-LAB7-ServiceServer)

### Architecture:
The implementation follows the following Architecture:
![Imagen](img/architecture)

### Components:
We have 2 EC2 instances on Amazon Web Services, each one have a Docker container running on port 8081 with the a web server made with spark framework.
![Imagen](img/maquinas)

the first server is secured with a login view, and you'll be only able to send requests to the second server if you are logged in, the login component works with cyphered passwords using MD5 Hash. 
Also both servers are secured with certificates, this means that the servers will be able to communicate only if each one has the other's certificate(Public Key) in its TrustStore and that's how it works,thanks to that the requests to the servers are only via HTTPS. Next, theres an image of how the requests are made:

- Requesting the Login Server(Browser):
![Imagen](img/requestLogin)
- Requesting Service server(Request Code):
![Imagen](img/requestService)
- Requesting the Login Server with HTTP (NOT WORK)
![Imagen](img/requestLoginHttp)

### EndPoints:
The available endpoints for the Login service are:
- /login.html (Static file for public requests)
- /secured/index.html (Static file only for logged users it calls to /secured/service endpoint)
- /secured/service (Makes an GET Request to Service Server)

And the service server have only one endpoint:
- /service (This endpoint returns the Service Server date)

### Certificates:
- Login server Certificate:
![Imagen](img/logincertificate)
- Service server Certificate:
![Imagen](img/servicecertificate)

### Docker containers in EC2 machines:
- Login Server
![Imagen](img/containerlogin)
- Service server
![Imagen](img/containerservice)

### DEMO:
The following video shows the results of the implementation. [VIDEO HERE](https://youtu.be/JdsTwXFex40)