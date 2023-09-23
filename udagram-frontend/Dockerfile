# # Use IONIC base image
# FROM beevelop/ionic:latest AS ionic

# # Create app directory in Docker
# WORKDIR /usr/src/app

# # Install app dependencies by copying
# # package.json and package-lock.json
# COPY package*.json ./

# # Install dependencies in Docker
# RUN npm install

# # Copy app from local environment into the Docker image
# COPY . .

# # Build app
# RUN ionic build

# FROM nginx:alpine

# #COPY www /usr/share/nginx/html
# COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html
### Build
FROM beevelop/ionic:latest AS ionic
## Create app directory
WORKDIR /usr/src/app
## Install app dependencies
## A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
RUN npm ci
## Bundle app source
COPY . .
RUN ionic build
### Run 
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html