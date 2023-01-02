# moresand
test

-----------------------------------------------------------------------------------------------------------------------------------------
Create a file called app.py with the following content:

print("Hello, World!")
--------------------------------------------------------------------------------------------------------------------------------------
create a file called Dockerfile in the app directory with the following content:

FROM python:3.8
COPY . /app
WORKDIR /app
CMD ["python", "app.py"]

This Dockerfile specifies that we want to use the Python 3.8 base image and copy the current directory into the /app directory inside the container. 
It also sets the working directory to /app and specifies that the default command should be to run the app.py script using the python command.

---------------------------------------------------------------------------------------------------------------------------------------
Create a file called nginx.conf with the following content:

events { }
http {
    server {
        listen 80;
        location / {
            proxy_pass http://hello-app:8080;
        }
    }
}

This configuration file specifies that Nginx should listen on port 80 and forward all requests to the hello-app container on port 8080.
-------------------------------------------------------------------------------------------------------------------------------------------
Create a file called Dockerfile in the nginx directory with the following content:

FROM nginx:latest
COPY nginx.conf /etc/nginx/nginx.conf
This Dockerfile specifies that we want to use the latest version of the Nginx base image and copy the nginx.conf file into the /etc/nginx directory inside the container.
----------------------------------------------------------------------------------------------------------------------------
Create a file called Dockerfile in the mysql directory with the following content:

FROM mysql:latest
ENV MYSQL_ROOT_PASSWORD password
VOLUME /var/lib/mysql

This Dockerfile specifies that we want to use the latest version of the MySQL base image and set the value of the MYSQL_ROOT_PASSWORD environment variable to password. It also declares a volume at the /var/lib/mysql directory, which will be used to store the data for the MySQL database.
------------------------------------------------------------------------------------------------------------------------------
Create a file called docker-compose.yml with the following content:

version: '3'
services:
  app:
    build: app
    expose:
      - "8080"
  nginx:
    build: nginx
    ports:
      - "80:80"
    depends_on:
      - app
  mysql:
    build: mysql
    environment:
      MYSQL_ROOT_PASSWORD: password
    volumes:
      - mysql-data:/var/lib/mysql

volumes:
  mysql-data:
	
This docker-compose.yml file specifies that we have three services: app, nginx, and mysql. It also defines the build context for each service and the appropriate configuration options
