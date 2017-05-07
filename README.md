# docker-course

### Listing images and containers

`docker image ls`

`docker container ls`

### Creating and Running containers

`docker container run -p hostPort:containerPort imageName:imageVersion`

`... --detach|-d`
> Runs the container in the background

`... -v localPath:containerPath`
> Creates a link between your local directory and a directory in the container, so you don't lose that data when the container is stopped 

`docker container run httpd:2.4`
> Create and run a container based on the image for the Apache HTTP Server version 2.4

### Creating images from a Dockerfile

`docker image build --tag setImageName:setImageVersion .` 
> The dot tells docker to look for a Dockerfile in the current directory

### Executing commands in a running container

`docker container exec apt-get update && apt-get install -y fortunes`

`docker container exec -it containerId|containerName /bin/bash`
> This will start an interactive shell with the container

### Copying files into a running container 

`docker container cp yourLocalFilePath containerName:containerDirectoryTarget`

`docker container cp page.html myImage:/usr/local/apache2/htdocs/`

### Sample Dockerfile

```
LABEL maintainer="miltonbecker@gmail.com"

# Base image
FROM node:boron

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install --production

# You can run any command with RUN, like RUN apt-get update && apt-get install -y fortunes

# Bundle app source
COPY . /usr/src/app

EXPOSE 8000

CMD [ "npm", "start" ]
```

