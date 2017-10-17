FROM postgres:9.5

VOLUME /var/lib/postgresql/data

COPY ./init-db.sql /docker-entrypoint-initdb.d/
