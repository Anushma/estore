# Use the official Node.js base image
FROM node:14-alpine AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json files
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the entire Angular project to the container
COPY . .

# Build the Angular application
RUN npm run build --prod

# Use a lightweight web server to serve the application
FROM nginx:alpine

# Copy the built Angular application to the Nginx web server directory
COPY --from=build /app/dist/estore-admin-dashboard-main /usr/share/nginx/html

# Expose port 80 to allow traffic to the web server
EXPOSE 80

# Start the Nginx web server
CMD ["nginx", "-g", "daemon off;"]
