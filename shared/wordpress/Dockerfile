# https://github.com/docker-library/wordpress
FROM wordpress:fpm-alpine
LABEL maintainer "https://github.com/yongxinL/Dockyard"

# install Nginx and supervisor
RUN apk add --no-cache \
    nginx \
    supervisor

# Create necessary directories
RUN mkdir -p /run/nginx \
    /var/log/supervisor \
    /etc/supervisor.d

# Copy Nginx configuration
COPY etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY etc/nginx/http.d/wordpress.conf /etc/nginx/http.d/default.conf

# Copy supervisor configuration
COPY etc/supervisord.conf /etc/supervisord.conf

# Expose HTTP port (Nginx)
EXPOSE 80

# Use supervisord as the main process
ENTRYPOINT []
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]