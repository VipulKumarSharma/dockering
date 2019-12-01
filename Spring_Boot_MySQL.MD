# Spring Boot on Docker connecting to MySQL Docker container

<b>1. Run the mysql container</b>

    docker pull mysql
    docker run --name mysql-standalone -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=test -e MYSQL_USER=sa -e MYSQL_PASSWORD=password -d mysql:5.6

<b>2. In the Spring Boot Application, use the same container name of the mysql instance in the application.properties</b>

    spring.datasource.url = jdbc:mysql://mysql-standalone:3306/test

<b>3. Create a `Dockerfile` for creating a docker image from the Spring Boot Application</b>
    
    FROM openjdk:8
    ADD target/users-mysql.jar users-mysql.jar
    EXPOSE 8086
    ENTRYPOINT ["java", "-jar", "users-mysql.jar"]

<b>4. Using the Dockerfile create the Docker image. From the directory of Dockerfile -</b> 

    docker build . -t users-mysql

<b>5. Run the Docker image (users-mysql) created in #4</b>

    docker build . -t users-mysql

<b>6. Create users-mysql container, which is linked to  mysql-standalone container</b>

    docker run -p 8086:8086 --name users-mysql --link mysql-standalone:mysql -d users-mysql
    
<b>7. Check containers</b>

    docker container ls
    
<b>8. Check container logs</b>
    
    docker logs <CONTAINER_ID>

## Useful Docker commands
    
    docker images
    
    docker container ls
    
    docker logs <container_name>

    docker container rm <container_name
    
    docker image rm <image_name
