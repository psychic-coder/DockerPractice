How to start with docker--->

1)Before setting up the docker we usually delete the node_modules folder
2)Then we create the file named "Dockerfile"

3)Inside the docker file we write the base image first
FROM node //this node will come from already uploaded images from docker and it will be the latest version of node , to use any other version of node we can do it as 
"node:20"

4)WORKDIR /myapp // --> this step is used to create a folder inside the container, inside which we will run the file

5)COPY . . //this is used to copy all the files from the project folder to the folder inside the working directory

6)RUN npm install //this is used to run the app

its optional)EXPOSE 5173 //we wrote here 5173 as this is the port on which this application runs 

7)CMD ["npm","start"] //we wrote the code in this way as by writing this way we are not running the project right now , and also there are two commands so we wrote it in this manner 


//so basically what we did we created an image using the first 4 commands and when we run the image the project is runned by the last command

//" docker build . " ---->//to create the image we wrote this in command line

// " docker image ls " --->//to check the image we created we can type this in command line

//"docker run ebce1a9aab3e " ---->//using this code we can run the image and "ebce1a9aab3e" this is the image id, but we cannot access the website in the browser as the project is running inside the container , so our browser is unable to access it 

//"docker ps"---> write this in the other terminal ,it only shows the running containers, from there we select the name of the container created 

//"docker ps -a"---> it  shows all the containers created

//docker rm container_name:--->it is used to remove a container

//"docker stop  quirky_zhukovsky"--->this command is used to stop the container with name "quirky_zhukovsky"

//"docker run -p 5173:5173 6ebeaaffef30"---->to solve the error we can use this command in this command we're binding the application which is running inside the container at the port 5173 ,  is binded to the port 5173 outside the container , the first 5173 is the port of the browser we are binding the second 5173 in the container

//"for vite builds we have to modify the dev script in the 
    "scripts": {
    "dev": "vite --host",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
"

//"docker run -d -p 5173:5173 6ebeaaffef30"//---> to run the docker in detached mode (in detached mode we can use the terminal even after starting the docker file )


//"docker run -d -p 5173:5173 6ebeaaffef30"---> we can write this command multiple times by changing the port number of the browser and we can create multiple containers from the same image 

//"docker run -d --rm -p 5176:5173 6ebeaaffef30"----> this container will run as we we will start but as we have given "--rm" so the container will get deleted automatically whenever we'll stop the container

//"docker run -d --rm --name "webapp" -p 5176:5173 6ebeaaffef30"----> using the name keyword we can even give name to the container which will be generated , as in this case we're giving the name "webapp"

//" docker build -t mywebapp:01 ."--> we can even give name to the image created and "01" represents the version

//"docker rmi mywebapp:02"-->this is how we can delete an image , in this case we gave the app name and the version

//" docker build -t mywebapp:02 . " ----> after we make any changes in our app we have only create a new image 

// " docker run -d --rm -p 5177:5173 mywebapp:02 " -->we can even create a container out of the image using the imagename and version 

//" docker pull python " --->this is the way how we can download a predefined image from the docker's website , we have to write the code in the terminal, but as this is a software and not a service , it will stop automatically
exx:-->
docker pull nginx --> this is a web server after pulling the image we can run this as " docker run -d -p 8080:80 nginx:latest  "


//" docker run -it image_id "---> to run an image in interactive mode we can write this command here "-it" makes it interactive  , interactive mode means we can type the inputs for the programm in terminal 


//Steps before pushing file to docker
//1)docker login 
//2)push files to the docker using the command
//3)we have to create an image of the same name as of the repo before pushing the image ex:-->" docker build -t hellroh/project_vite123:01 . "
 //4)" docker push hellroh/project_vite123:01  " --->in this command we pushed the file to the docker



//" docker tag old_name new_name"--> we can even rename an already created image , 
ex:--> "docker tag mywebapp:02 booyakah:03"


//"  docker pull hellroh/project_vite123:02"--->to pull an image from docker we type this and then we can run that via--
 " docker run -d --rm -p 5177:5173 hellroh/project_vite123:02 "


 //"docker run -it --rm -v myvolume:/myapp/ d48d7ee6dddc"--> the "-v" is used to create a volume in which the data will be stored after we stop the program and "myvolume:/myapp/" this is the path where the data is stored, so basically this file created is outside the container and stays present even afte the image is stopped

 //"docker volume ls"--> it gives the list of the volume created with the name and the driver address


 //"docker volume inspect volume_name"-->it gives the details regarding the myvolume


 //Bind Mount in docker volume
 docker run -v /Users/mycomputer/projects/servers.txt:/myapp/servers.txt --rm image_id---->
 using this we can bound the servers.txt present inside the container to be mounted to the original servers.txt file present in the local environment " /Users/mycomputer/projects/servers.txt "---->absolute path of the file in local environment and 
 " /myapp/servers.txt  "---->address of the file present in the image created , 
 by doing this if we make any changes in the file in the local environment then the change will be reflected in the image created and we are not needed to create the image everytime and also if we checek we 're not creating any volume as we're mounting the file from the local system 

 //" .dockerignore "-->its similar to gitignore


 //" Communication From/To containers "
 
1)Working with api's-->
 To fetch a data from the data from the outer world--

in the below example picture we are installing an external package which is not there predefined in the docker in python , similar will be for the other applications

//////////
![Alt text](<Screenshot 2024-06-28 at 2.40.47 PM.png>)
//////////

after this the file will work

2)"Communication between Containers and local db"

/////////////
the below screenshot shows the connection between a database and a python code 

![Alt text](<Screenshot 2024-06-28 at 2.48.32 PM.png>)
![Alt text](<Screenshot 2024-06-28 at 2.49.29 PM.png>) 
![Alt text](<Screenshot 2024-06-28 at 2.49.37 PM.png>)

//////////////so now if we'll try to connect then it will show an error , so to correct the error we have to make a change in the connection in the host name to ==>" host.docker.internal " ------

![Alt text](<Screenshot 2024-06-28 at 2.54.12 PM.png>)
///////////////


3)Connection between one container and the other 
ex:-->in this scenario we're connecting the mysql in one container and the python in the other container 
//in the below code we're setting up the mysql in the terminal after pulling the code 
docker run -d --env MYSQL_ROOT_PASSWORD="root" --env MYSQL_DATABASE="userinfo" --name mysqldb mysql

//"docker inspect mysqldb" ---->this code gives all the details regarding the container - "mysqldb"-it is the name of the container 

now as we have to connect to the mysql present in a different container we will be using the ip address of the "mysqldb " container as the host name 

////in the below code we have added the ip as the host name 
![Alt text](<Screenshot 2024-06-28 at 4.47.33 PM.png>)
//////////

now we can build this container as well and if we'll try to connect them now it will work
and they run the code successfully


////////Docker Network
<br/>
docker network create mongo-network///---->first we have to create a mongo network before connecting it to the network
<br/>


docker network create my-net ------>it is used to create a network

docker network ls --->gives the list of the network


///docker run -d --env MYSQL_ROOT_PASSWORD="root" --env MYSQL_DATABASE="userinfo" --name mysqld --network my-net mysql ///-----> in this command we're creating an image of the mysql and connecting it to the network and " --network my-net " using this command we have conneted it to the my-net database

as we're using the network now we only have to give the name of the image in the place of host for connecting to the mysql

///////
![Alt text](<Screenshot 2024-06-28 at 5.09.32 PM.png>)
//////


and after creating the image after the above changes we habe to create a container for it using the below code
"docker run -it --rm --network my-net image_id"





//Docker Compose -->its a configuration file to manage multiple containers running on same machine...

to run the docker compose file we write the below code

"docker-compose up"--->we started the compose file and "docker-compose" this is the name of the compose file
"docker-compose down"--->"docker-compose" this is used to stop the compose file
"docker-compose up -d"-->to start the docker compose in detached mode


////docker compose for multiple containers
docker-compose-->the goal is to set up a multi-container application with a MySQL database and a ReactJS web application. The configuration ensures that the web application (myjs) only starts after the database (mysqldb) is fully operational.

![Alt text](<Screenshot 2024-06-28 at 7.06.07 PM.png>)

///////////

we can even run the services present in the docker-compose file one by one -->
"docker-compose run -d myjs"  ---->" myjs " is the name of the service

//all the services present in the docker-compose file are part of a network

![Alt text](<Screenshot 2024-06-28 at 7.29.07 PM.png>)

////////////

 "docker-compose down -v"-->this command stops the docker-compose and lowers down the network

 //////////

 // we can even bind the file in our container to the file in our local system , in this case we used the " volumes: " ,, we binded the server.txt file in our local repo to the server.txt file in the myapp repository

//////
 ![Alt text](<Screenshot 2024-06-28 at 7.34.08 PM.png>)
//////


/////
docker logs container_name --->logs all the info when we start the container
////


//////
docker run -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password -d mongo ---->we can give as many environment variables we want by using the "-e"
//////

//////

//////

/////
<br/>

docker run -d \
-p 8081:8081 \
-e ME_MONGO_INITDB_ROOT_USERNAME=admin \
-e ME_MONGO_INITDB_ROOT_PASSWORD=password\
-e ME_CONFIG_MONGODB_SERVER=mongodb \
--net mongo-network \
--name mongo-express \
mongo-express------> in this code in the name of the server we have to give the name of the mongodb image we created , so that this container can connect to the mongodb container , the "\" is used to prevent the code from breaking while we write the code in multiple lines in the terminal

<br/>
\\\\\\

