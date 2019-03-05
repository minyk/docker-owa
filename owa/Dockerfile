FROM nginx:1.15

RUN apt update && apt install -y php-fpm php7.0-mysql php7.0-imap php7.0-mbstring curl runit

ARG OWA_VERSION
ENV OWA_VERSION ${OWA_VERSION}
ADD https://github.com/padams/Open-Web-Analytics/archive/${OWA_VERSION}.tar.gz  /owa-${OWA_VERSION}.tar.gz
RUN tar zxf /owa-${OWA_VERSION}.tar.gz && rm -rf /app && ln -sf /Open-Web-Analytics-${OWA_VERSION} /app && mkdir -p /var/lib/php/session && chown -R www-data:www-data /Open-Web-Analytics-${OWA_VERSION} /app /var/lib/php/session
COPY config/owa-config.php.tpl  /app/owa-config.php.tpl
COPY nginx/default.conf  /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf    /etc/nginx/nginx.conf
#COPY php/www.conf        /etc/php-fpm.d/www.conf
COPY php/timezone.ini    /etc/php/7.0/fpm/conf.d/timezone.ini
#COPY php/php.ini         /etc/php.ini

# Add runsvdir
ADD services /services

# Add Tini
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

# Add envtpl from https://github.com/subfuzion/envtpl
ADD envtpl-linux-amd64 /usr/bin/envtpl

# ENV for OWA
ENV OWA_DB_TYPE        "mysql"
ENV OWA_DB_HOST        "localhost:3306"
ENV OWA_DB_NAME        "owa"
ENV OWA_DB_USER        "owa"
ENV OWA_DB_PASSWORD    "owa"
ENV OWA_PUBLIC_URL     "http://localhost:80/"
ENV OWA_NONCE_KEY      "owanoncekey"
ENV OWA_NONCE_SALT     "owanoncesalt"
ENV OWA_AUTH_KEY       "owaauthkey"
ENV OWA_AUTH_SALT      "owaauthsalt"
ENV OWA_ERROR_HANDLER  "development"
ENV OWA_LOG_PHP_ERRORS "false"
ENV OWA_CACHE_OBJECTS  "true"

CMD ["runsvdir", "-P", "/services"]
