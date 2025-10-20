# Use the official lightweight NGINX image.
FROM nginx:alpine

# Remove the default NGINX configuration file.
RUN rm /etc/nginx/conf.d/default.conf

# Copy our custom configuration into the container.
COPY nginx.conf /etc/nginx/nginx.conf
