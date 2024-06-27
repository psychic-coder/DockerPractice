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

