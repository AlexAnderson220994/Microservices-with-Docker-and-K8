# Use an official Node.js runtime as the base image
FROM node:12
 
# Set the working directory within the container
WORKDIR /usr/src/app
 
# Copy package.json and package-lock.json to the container
COPY package*.json ./
 
# Install application dependencies
RUN npm install
 
# Copy the rest of the application code to the working directory
COPY . .
 
# Expose the port that the app runs on
EXPOSE 3000
 
# Define the command to run the app
CMD [ "node", "app.js" ]
