# Stage 1: Build React App
FROM node:18-alpine AS build

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy the rest of the app's source code and build the project
COPY . .
RUN npm run build

# Stage 2: Serve React App
FROM nginx:stable-alpine

# Copy build output to Nginx's HTML folder
COPY --from=build /app/build /usr/share/nginx/html

# Expose the port Nginx will serve on
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
