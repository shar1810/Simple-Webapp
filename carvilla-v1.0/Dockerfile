# Use Nginx as the base image
FROM nginx:alpine

# Remove default nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy your static web app files into Nginx's html directory
COPY carvilla-v1.0/ /usr/share/nginx/html/

# Expose port 80 for HTTP traffic
EXPOSE 80

# Start Nginx in foreground
CMD ["nginx", "-g", "daemon off;"]
