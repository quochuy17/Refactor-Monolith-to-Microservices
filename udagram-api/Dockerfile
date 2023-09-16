FROM node:12 AS first_stage
# Set the working directory for any further commands
WORKDIR /usr/src/app
# Make somes copies file into app directory
COPY . /usr/src/app
# Make installation with dependencies
RUN npm install
# run to build process  
RUN npm run build
# Make some definition of node image
FROM node:12-slim
# Make some settings of env variables supplied to our container to be used from code
ENV POSTGRES_USERNAME=$POSTGRES_USERNAME
ENV POSTGRES_PASSWORD=$POSTGRES_PASSWORD
ENV POSTGRES_HOST=$POSTGRES_HOST
ENV POSTGRES_DB=$POSTGRES_DB
ENV AWS_BUCKET=$AWS_BUCKET
ENV AWS_REGION=$AWS_REGION
ENV AWS_PROFILE=$AWS_PROFILE
ENV JWT_SECRET=$JWT_SECRET
ENV URL=$URL
ENV BACKEND_PORT=$BACKEND_PORT
# Create an app directory
WORKDIR /usr/src/app
# Make some copies the app source 
COPY --from=first_stage /usr/src/app/www/ /usr/src/app/
COPY --from=first_stage /usr/src/app/ /usr/src/app/
# Remove unessential files 
RUN rm -rf www && rm -rf src
# Make some definitions of network port 
EXPOSE $BACKEND_PORT
# Make some definition of Docker image
CMD ["node", "server.js"]