# Containerizing a React Application with Docker 🐳

## Overview

This guide walks you through the steps to containerize a React application using Docker. By containerizing your app, you ensure consistency across different environments and streamline the deployment process.


## Step 1: Set Up Your React Application

If you don't already have a React app, you can create one using the following commands:

```bash
npx create-react-app my-react-app
cd my-react-app
```

## Create Dockerfile in root directory 

add the following script to your dockerfile

```bash

# Use the official Node.js image as the base image

FROM node:18

# Set the working directory

WORKDIR /app

# Copy package.json and package-lock.json

COPY package*.json ./

# Install dependencies

RUN npm install
```

```bash

# Copy the rest of the application code

COPY . .

# Build the application

RUN npm run build

# Expose port 3000

EXPOSE 3000

# Command to run the application

CMD ["npm", "start"]
```

## Step 3: Build the Docker Image

```bash
docker build -t my-react-app .
```

## Step 4: Run the Docker Container


```bash
docker run -p 3000:3000 my-react-app
```
## Step 5: Access Your Application

```bash
http://localhost:3000/
```
