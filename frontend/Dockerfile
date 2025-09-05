# Stage 1: Build the React/Vue/Svelte application
FROM node:18 as build

# Set the working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application source code
COPY . .

# Build the application for production
# This creates a 'dist' or 'build' folder with static files
RUN npm run build

# Stage 2: Serve the static files with a lightweight Nginx server
FROM nginx:stable-alpine

# Copy the build output from the 'build' stage
# Make sure the source path (/app/dist) matches your build output directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 for the Nginx server
EXPOSE 80

# The default Nginx command will start the server automatically
CMD ["nginx", "-g", "daemon off;"]
