# joomla-docker-compose-project
THis project is for to setup complete infrastructure of **JOOMLA!** by using a single command.
## Technologies that i used
Redhat8, Docker, docker-compose, Containerization, Storage , Networking.
JOOMLA software and MySQL software.
### JOOMLA!
Joomla is an open source platform on which Web sites and applications can be created. It is a content management system (CMS) which connects your site to a MySQLi, MySQL, or PostgreSQL database in order to make content management and delivery easier on both the site manager and visitor.
### MySQL
MySQL is the world's most popular open source database. With its proven performance, reliability and ease-of-use, MySQL has become the leading database choice for web-based applications, covering the entire range from personal projects and websites, via e-commerce and information services, all the way to high profile web properties including Facebook, Twitter, YouTube, Yahoo! and many more.
## My Purpose for creating this project
If we have to work on joomla for creating web application framework, we will have to be create first complete infrastructure for joomla.

In normal way, first we download the images by docker command.

$ *`docker pull mysql:5.7`*    and   $ *`docker pull joomla:latest`*  

then we start MySQL container by this heay command.

 $ *`docker run -dit -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_USER=gudiya -e MYSQL_PASSWORD=1@Sulekha -e MYSQL_DATABASE=sqldb -v mystorage:/var/lib/mysql --name mysqlos mysql:5.7 `*  
 
then we start joomla we start joomla container by this command.

$ *`docker run -it -e JOOMLA_DB_HOST=mysqlos -e JOOMLA_DB_USER=gudiya -e JOOMLA_DB_PASSWORD=1@Sulekha -e JOOMLA_DB_NAME=sqldb -v jostorage:/var/www/html -p 8081:80 --link mysqlos --name joomlaos joomla:latest`* 

Whenever we will start working on joomla before that we will have to be run these very heavy command again and again with providing lots of details like user name, password,database name, container name, image name. 
this is very lengthy process.

So for trubleshooting this problem i have created my project, from this we can create complete infrastructure in a single command.

## PROCEDURE
I have created this project on **Redhat8 linux operating system**. in my *OS* i have install **docker** and **docker-compose** software.

link for download the docker-compose:- https://docs.docker.com/compose/install/

Before start discussion a very good thing of my project is we don't need to download images of JOOMLA! and MySQL. images will start downloading automatically at the time of running the yml file. 

1. first we need to create a YAML file. I have used vim editor to create this file and name of the file always should be ***docker-compose.yml***

$ *`vim docker-compose.yml`*

write all the code in this file *docker-compose.yml* which is written below on the picture.

![Screenshot from 2020-04-29 03-51-35](https://user-images.githubusercontent.com/64317049/80553796-b4fb2f80-89e8-11ea-95f5-d771ce02d964.png)

In the above image lots of things are there like version,services,image,enviroment and etc.
  #### -Version
  There are lots of version of compose file but i am using here version 3.
  #### -Services
  It will start containers with their name. here i have given my MySQL container name is ***mysqlos*** and JOOMLA container name is ***joomlaos***.
  #### -Image
  In this we are writting those images name which we want to use. here i have used images ***mysql:5.7*** and ***joomla:latest*** these version are one of the more stable version.
  #### -Volumes
  It will save your all the data so that after stop your container, data will not lose. I have given MySQL volumes name
is ***mystorage***   and ***/var/lib/mysql*** where all the data stores. we can check this using 

$ *`docker inspect mysql:5.7`* 

if image is download in your OS.same as with joomla.
  #### -Restart
  If any of the container is stop , it will start again.
  #### -Enviroment 
  In the some of the images, ***entrypoint*** is required at the time of runing the conatainer. there are some predefined variables name like MYSQL_ROOT_PASSWORD, MYSQL_USER and etc. we will have to be fill this details. same as with joomla.
  #### -depends_on 
  Here we will have to give our database conatainer name so that joomla can store the data. here i am using ***mysql:5.7*** database and name of container is ***mysqlos***.
  #### -port
  port number is a way to identify a specific proccess so that we can access our WebApp. we can use any port number between 1 to 65535 but only condition is that is should not be running. to check this we use command 
  
  $ *`netstat -tnlp`*.

2. Run the command

$ *`docker-compose up`*

it will look something like this

![Screenshot from 2020-04-29 03-54-36](https://user-images.githubusercontent.com/64317049/80544766-61c8b300-89cf-11ea-902a-065bc4294301.png)

3. Run the command

$ *`docker-compose ps`*

it will show you all the container is running or not.

![Screenshot from 2020-04-29 03-59-47](https://user-images.githubusercontent.com/64317049/80544943-c8e66780-89cf-11ea-949f-87511219a709.png)

4. Running process of conatainers

![Screenshot from 2020-04-29 04-00-04](https://user-images.githubusercontent.com/64317049/80544983-e87d9000-89cf-11ea-8f45-0f485f163971.png)

5. Goto to browser and then access it via  

$ *`http://localhost:8081`*   or  $ *`http://host-ip:8081`*

![Screenshot from 2020-04-29 04-02-47](https://user-images.githubusercontent.com/64317049/80545054-1531a780-89d0-11ea-8ee8-9994d7a01bcb.png)

6. Now we can see the JOOMLA page

![Screenshot from 2020-04-29 04-01-52](https://user-images.githubusercontent.com/64317049/80545161-49a56380-89d0-11ea-971b-c489c2eba0f4.png)

7. If we want to stop containers, command is   $ *`docker-compose stop`*. after stoping the containers clear the enviroment using   $ *`docker rm -f $(docker ps -a -q)`* so that we can start our complete setup again and again by using only a singal command   $ *`docker-compose up`*.

#### Everything is done!

### THANK YOU!

