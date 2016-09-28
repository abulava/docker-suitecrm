FROM php:5.6-apache

# SugarCRM 7.7.4
ENV DOWNLOAD_URL http://kent.dl.sourceforge.net/project/suitecrm/SuiteCRM-7.7.4.zip
ENV DOWNLOAD_FILE suitecrm-7.7.4-max.zip
ENV EXTRACT_FOLDER SuiteCRM-7.7.4
ENV WWW_FOLDER /var/www/html
ENV WWW_USER www-data
ENV WWW_GROUP www-data

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y libcurl4-gnutls-dev libpng-dev libssl-dev libc-client2007e-dev libkrb5-dev unzip cron re2c python tree && \
    docker-php-ext-configure imap --with-imap-ssl --with-kerberos && \
    docker-php-ext-install mysql curl gd zip mbstring imap && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /tmp

RUN curl "${DOWNLOAD_URL}" > $DOWNLOAD_FILE && \
  unzip $DOWNLOAD_FILE && \
  rm $DOWNLOAD_FILE && \
  rm -rf ${WWW_FOLDER}/* && \
  cp -R ${EXTRACT_FOLDER}/* ${WWW_FOLDER}/ && \
  chown -R ${WWW_USER}:${WWW_GROUP} ${WWW_FOLDER}/* && \
  chown -R ${WWW_USER}:${WWW_GROUP} ${WWW_FOLDER}

EXPOSE 80
ENTRYPOINT ["/usr/local/bin/init.sh"]
