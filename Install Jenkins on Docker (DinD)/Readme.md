## Install docker on centos
 - ./install-docker.sh

## Create Docker Network
 - docker network create jenkins

## Run Docker Commands inside Jenkins Nodes , Download and run Docker:dind
docker run \
  --name y-technologies-jenkins \
  --rm \
  --detach \
  --privileged \
  --network jenkins \
  --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind \
  --storage-driver overlay2

** Note: Must have Dockerfile before this steps. **

## Build the Dockerfile
 
   - docker build -t ytechnologies-jenkins .

## Run the Jenkins Container

  docker run \
  --name ytechnologies-jenkins \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  ytechnologies-jenkins

## Check the Password
	
   - docker exec -it 12959e251ec8 cat /var/jenkins_home/secrets/initialAdminPassword

## **Access the Jenkins URL**
	http://youripaddress:8080/