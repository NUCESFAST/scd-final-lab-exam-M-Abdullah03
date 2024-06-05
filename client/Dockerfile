FROM node:14 as build
# Set working directory
WORKDIR /app
# Copy package.json and package-lock.json
COPY package*.json ./
# Install dependencies
RUN npm install
RUN npm install -g serve

# Copy the rest of the files
COPY . .
# Build the app
RUN npm run build

EXPOSE 3000
CMD ["serve", "-s", "build"]
