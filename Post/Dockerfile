# Use an official Node runtime as the base image
FROM node:14

# Set the working directory in the container to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install any needed packages specified in package.json
RUN npm install

# Bundle app source
COPY . .

# Make port (roll no 1215) available to the world outside this container
EXPOSE 4002

# Run the app when the container launches
CMD ["node", "index.js"]