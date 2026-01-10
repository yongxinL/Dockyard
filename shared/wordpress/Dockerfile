# https://github.com/docker-library/wordpress
FROM wordpress:fpm-alpine
LABEL maintainer "https://github.com/yongxinL/Dockyard"

# install Nginx and supervisor
RUN apk add --no-cache \
    nginx \
    shadow \
    supervisor

# Align www-data UID/GID with host to fix permission issues
ARG WWW_DATA_UID=1000
ARG WWW_DATA_GID=1000

# Modify www-data user and group in the container
RUN groupmod -g $WWW_DATA_GID www-data && \
    usermod -u $WWW_DATA_UID -g $WWW_DATA_GID www-data

# Copy and update PHP configuration
RUN cp ${PHP_INI_DIR}/php.ini-production ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^allow_url_fopen.*/allow_url_fopen = off/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^max_execution_time.*/max_execution_time = 300/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.enable=.*/opcache.enable=1/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.enable_cli=.*/opcache.enable_cli=1/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.memory_consumption=.*/opcache.memory_consumption=64/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.interned_strings_buffer=.*/opcache.interned_strings_buffer=8/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.max_accelerated_files=.*/opcache.max_accelerated_files=8000/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.max_wasted_percentage=.*/opcache.max_wasted_percentage=5/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.validate_timestamps=.*/opcache.validate_timestamps=1/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.revalidate_freq=.*/opcache.revalidate_freq=60/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^;opcache.fast_shutdown=.*/opcache.fast_shutdown=1/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^post_max_size.*/post_max_size = 768M/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^session.use_trans_sid.*/session.use_trans_sid = 0/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^upload_max_filesize.*/upload_max_filesize = 768M/' ${PHP_INI_DIR}/php.ini && \
    sed -i 's/^zlib.output_compression.*/zlib.output_compression = On/' ${PHP_INI_DIR}/php.ini

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