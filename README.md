# docker-course

## Listing images and containers

`docker image ls`

`docker container ls`

## Running containers

`docker container run -p hostPort:containerPort imageName:imageVersion`

## Creating images from a Dockerfile

`docker image build --tag setImageName:setImageVersion .` 
> the dot tells docker to look for a Dockerfile in the current directory

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

