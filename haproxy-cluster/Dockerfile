# Use an official HAProxy image as a parent image.
FROM haproxy:latest

# Switch to the root user to install packages.
# The base haproxy image runs as a non-root user by default.
USER root

# Install keepalived and curl (for healthcheck).
# We update the package list and install keepalived without installing recommended packages to keep the image small.
RUN apt-get update && apt-get install -y --no-install-recommends keepalived curl && apt-get clean && rm -rf /var/lib/apt/lists/*

# Argument to receive the keepalived config file name from docker-compose build args.
ARG KEEPALIVED_CONFIG

# Copy the HAProxy configuration file into the container.
COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

# Copy the Keepalived configuration file into the container.
COPY ${KEEPALIVED_CONFIG} /etc/keepalived/keepalived.conf

# Copy the entrypoint script, make it executable, and set it as the container's entrypoint.
COPY entrypoint.sh /entrypoint.sh
# Ensure the script has Unix-style line endings (LF) instead of Windows (CRLF).
# This prevents "no such file or directory" errors when running the script.
RUN sed -i 's/\r$//' /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]