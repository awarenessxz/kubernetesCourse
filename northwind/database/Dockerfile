# get mysql images
FROM mysql:5.7
#FROM mysql@sha256:bf17a7109057494c45fba5aab7fc805ca00ac1eef638dfdd42b38d5a7190c9bb

#ENV MYSQL_ROOT_PASSWORD=changeit MYSQL_DATABASE=northwind
ENV MYSQL_ROOT_PASSWORD=changeit MYSQL_PORT=3306 MYSQL_DB_PATH=/var/lib/mysql

ADD 0-northwind-default-current-timestamp.sql /docker-entrypoint-initdb.d
ADD 1-northwind-data.sql /docker-entrypoint-initdb.d

# Anything Above is for building the image
# Anything Below is for running the image

#healthcheck (not the best healthcheck) -- need to run mysql client and perform a simple select
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
    CMD mysqladmin ping -uroot -p${MYSQL_ROOT_PASSWORD} || exit 1

EXPOSE ${MYSQL_PORT}

# the volume in the container
VOLUME ${MYSQL_DB_PATH}
