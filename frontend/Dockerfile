# # Use an official Node.js runtime as a parent image
# FROM node:14

# # Set the working directory in the container
# WORKDIR /app

# # Copy package.json and package-lock.json
# COPY package*.json ./

# # Install dependencies
# RUN npm install

# # Copy the rest of the application code
# COPY . .

# # Build the app
# RUN npm run build

# # Use an Nginx container to serve the build
# FROM nginx:alpine
# COPY --from=0 /app/build /usr/share/nginx/html

# # Expose port 80
# EXPOSE 80

# # Start Nginx
# CMD ["nginx", "-g", "daemon off;"]


# Dockerfile for React frontend
#FROM node:14-alpine as build
#WORKDIR /app
#COPY package.json ./
#RUN npm install
#COPY . .
#RUN npm run build

#FROM nginx:alpine
#COPY ./nginx.conf /etc/nginx/nginx/conf.d/nginx.conf
#EXPOSE 80
#CMD ["nginx", "-g", "daemon off;"]


# Stage 0, "build-stage", based on Node.js, to build and compile the frontend
FROM node:20 as build-stage

WORKDIR /app

COPY package*.json /app/

RUN npm install

COPY ./ /app/

ARG VITE_API_URL=${VITE_API_URL}

RUN npm run build


# Stage 1, based on Nginx, to have only the compiled app, ready for production with Nginx
FROM nginx:1

COPY --from=build-stage /app/dist/ /usr/share/nginx/html

COPY ./nginx.conf /etc/nginx/conf.d/default.conf
COPY ./nginx-backend-not-found.conf /etc/nginx/extra-conf.d/backend-not-found.conf
