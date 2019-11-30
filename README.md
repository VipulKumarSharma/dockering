# Dockering


## Docker Commands

### Build the image
    
    docker build .

### Download (if not available) Image, create container & execute the container. 
You can create [n] no of copies of images :

    docker run <IMAGE_ID>
    docker run mongo

### Check running containers
    
    docker ps

### To enter a docker images and run command interactively :

    docker exec -it <CONTAINER_ID> sh
    docker exec -it 980b788af773 bash    

### To enter a image & execute some commands we have few methods :

* Start the container & run command interactively
    
        docker start 980b788af773
        docker exec -it 980b788af773 bash
    
* Directly run docker image with command 
[ It is not an advised approach, which can override the default behaviour of container initialization & might cause problems ]

        docker run -it mongo bash
    
### Name & tag the Image
    
    docker build -t <DOCKER_USERNAME>/<IMAGE_NAME>:v1 .
    name :- <DOCKER_USERNAME>/<IMAGE_NAME>
    tag  :- :v1
    
    docker build -t tysonvks/mymongo:latest .

### Run Image using name:tag
    
    docker run tysonvks/mymongo:latest


<hr>


### Run Docker image with command :

    docker run busybox ls -latr

### List all containers with status :

    docker ps --all

### Launch a previously stopped container :

    docker start <CONTAINER_ID>
    docker start 980b788af773

### Stop the running container using id :

    docker stop 980b788af773

### Instantly kill the running container using id :

    docker kill 980b788af773




## Docker Hub commands

### Login to docker CLI
    
    docker login -u tysonvks -p $DOCKERHUB_TOKEN

### Get image from Docker Hub :

    docker pull busybox
    
### Add tag to your image
    
    docker tag <CONTAINER_ID> tysonvks/cloud-foundry-app:v1

### Push Docker image to Docker Hub

    docker push tysonvks/cloud-foundry-app
    
    
    
    
## Github Package Registry Commands

### Add Dockerfile in project's root directory
    
    FROM openjdk:8-jdk-alpine
    COPY target/cloud-foundry-app.jar cloud-foundry-app.jar
    EXPOSE 8080
    ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "cloud-foundry-app.jar"]
    
### Add code & build the project

    mvn clean install
    
### Build docker image (with name mentioned in Dockerfile) & check the same

    docker build . -t cloud-foundry-app:v1
    docker images
    
### Add Tag to docker image

    docker tag cloud-foundry-app:v1 docker.pkg.github.com/vipulkumarsharma/cloud-foundry-app/cloud-foundry-app:v1

### Login to github docker repo (using Github Token keys)</b>

    docker login docker.pkg.github.com -u VipulKumarSharma -p <GH_KEY>
    
### Push docker image to github package registry</b>

    docker push docker.pkg.github.com/vipulkumarsharma/cloud-foundry-app/cloud-foundry-app:v1

<i>Note : Use account name in lowercase only (in URL & tagging)</i>

### Run Docker image

    docker run cloud-foundry-app:v1 -p 8080:8080
    
### URL for locally running app in container : 
    
[http://172.17.0.2:8080](http://172.17.0.2:8080)
