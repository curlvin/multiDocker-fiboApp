# use alpine version of node as base image
FROM node:alpine as builder

# specify the working directory
WORKDIR /app

#copy over file to  working directory above(./)
COPY ./package.json ./

#install all dependencies into that working directory
RUN npm install

#copy over everything else into working directory
COPY . .

# use this as your primary command in the container
RUN npm run build


#include inginx in this image as well
FROM nginx

#open port for incoming request to nginx
EXPOSE 3000

#replace the target file wth this file
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

#copy over files from builder's build dir  into the nginx directory
COPY --from=builder /app/build /usr/share/nginx/html