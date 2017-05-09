# docker-course - notes

## General info

`docker info`

## Listing images and containers

`docker images -a`

`docker ps -a`

## Creating and Running containers

`docker container run -p hostPort:containerPort imageName:imageVersion`

`docker container run httpd:2.4`
> Create and run a container based on the image for the Apache HTTP Server version 2.4

`... --detach|-d`
> Runs the container in the background

`... --name aName`
> Sets a name for the container, so we can latter reference to it using its name instead of its id

`... --rm`
> Deletes the container when it stops running

### Volume mapping 

`... -v localPath:containerPath`
> Creates a link between your local directory and a directory in the container, so you don't lose that data when the container is stopped 

## Creating images from a Dockerfile

`docker image build --tag setImageName:setImageVersion .` 
> The dot tells docker to look for a Dockerfile in the current directory

## Executing commands in a running container

`docker container exec apt-get update && apt-get install -y fortunes`

`docker container exec -it containerId|containerName /bin/bash`
> This will start an interactive shell with the container

## Copying files into a running container 

`docker container cp yourLocalFilePath containerName:containerDirectoryTarget`

`docker container cp page.html myImage:/usr/local/apache2/htdocs/`

## Sample Dockerfile

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

