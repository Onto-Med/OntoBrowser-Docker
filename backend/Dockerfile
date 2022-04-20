FROM postgres:10

ENV POSTGRES_DB ontobrowser

COPY *.sql /docker-entrypoint-initdb.d/
COPY *.sh /docker-entrypoint-initdb.d/

EXPOSE 5432