# Use an official Nginx runtime as a parent image
FROM nginx:stable


# Copy the HTML, CSS, and JavaScript files into the container
COPY ui/ /usr/share/nginx/html
#Copy configs
COPY conf /etc/nginx

# Expose port 80 for the Nginx server
EXPOSE 80

# Start Nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]
