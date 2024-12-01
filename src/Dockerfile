# Use official Node.js image to build the app
FROM node:16 AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Use a lightweight web server to serve the built app
FROM nginx:alpine

# Copy the build output from the previous stage to the nginx directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 to serve the React app
EXPOSE 3000

# Start the nginx server
CMD ["nginx", "-g", "daemon off;"]
