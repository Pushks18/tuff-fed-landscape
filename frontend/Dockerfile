### STAGE 1: Build the React application ###
FROM node:18 as build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the frontend source code
COPY . .

# Build the application for production. This creates a 'dist' or 'build' folder.
RUN npm run build


### STAGE 2: Serve the built application with Nginx ###
FROM nginx:stable-alpine

# Copy the static files from the 'build' stage to the Nginx server directory
# IMPORTANT: If your build output is in a 'build' folder instead of 'dist', change '/app/dist' to '/app/build'
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 for the Nginx web server
EXPOSE 5173

# The default command for the Nginx image will start the server automatically.
# We add a command to make it run in the foreground.
CMD ["nginx", "-g", "daemon off;"]

