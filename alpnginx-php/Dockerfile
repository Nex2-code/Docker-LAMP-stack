FROM alpine
RUN apk update && apk add nginx
RUN apk add php-fpm \
    php-soap \
    php-openssl \
    php-gmp \
    php-pdo_odbc \ 
    php-json \
    php-dom \
    php-pdo \
    php-zip \
    php-pdo_pgsql \ 
    php-bcmath \
    php-gd \
    php-odbc \
    php-gettext \ 
    php-xmlreader \
    php-xmlrpc \
    php-bz2 \ 
    php-iconv \
    php-pdo_dblib \
    php-curl \
    php-ctype
RUN apk add supervisor && mkdir /var/www/html
RUN touch index.php && echo "hello" > /var/www/html/index.php && sed -i '1i <?php echo "Hello"; echo "<br>"; echo "Hostname:"; echo gethostname();?>' /var/www/html/index.php 
RUN sed -i '1!d' /var/www/html/index.php && mkdir -p /run/nginx && sed -i "s|;listen.owner\s*=\s*nobody|listen.owner = ${PHP_FPM_USER}|g" /etc/php7/php-fpm.conf && sed -i "s|;listen.group\s*=\s*nobody|listen.group = ${PHP_FPM_GROUP}|g" /etc/php7/php-fpm.conf && sed -i "s|;listen.mode\s*=\s*0660|listen.mode = ${PHP_FPM_LISTEN_MODE}|g" /etc/php7/php-fpm.conf && sed -i "s|user\s*=\s*nobody|user = ${PHP_FPM_USER}|g" /etc/php7/php-fpm.conf && sed -i "s|group\s*=\s*nobody|group = ${PHP_FPM_GROUP}|g" /etc/php7/php-fpm.conf && sed -i "s|;log_level\s*=\s*notice|log_level = notice|g" /etc/php7/php-fpm.conf && sed -i 's/include\ \=\ \/etc\/php7\/fpm.d\/\*.conf/\;include\ \=\ \/etc\/php7\/fpm.d\/\*.conf/g' /etc/php7/php-fpm.conf
COPY default.conf /etc/nginx/http.d/default.conf
COPY supervisord.conf /etc/supervisord.conf
EXPOSE 80 
CMD ["/usr/bin/supervisord"]
