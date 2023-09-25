# Use an official Nginx runtime as a parent image
FROM nginx:alpine

# Copy (all) the HTML, CSS, and JavaScript files into the container
COPY . /usr/share/nginx/html

# Explictly copy files to html
COPY favicon.ico /usr/share/nginx/html/
COPY index.html /usr/share/nginx/html/
COPY main.css /usr/share/nginx/html/
COPY main.js /usr/share/nginx/html/

# Copy config
RUN mkdir /etc/nginx/configs
COPY configs/config.json /etc/nginx/configs/config.json

COPY configs/config.json /usr/share/nginx/html/configs

# Expose port 80 for the Nginx server
EXPOSE 80

# Start Nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]
