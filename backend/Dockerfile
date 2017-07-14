FROM postgres:9

ENV POSTGRES_PASSWORD ontobrowser
ENV POSTGRES_USER ontobrowser
ENV POSTGRES_DB ontobrowser

COPY *.sql /docker-entrypoint-initdb.d/
COPY *.sh /docker-entrypoint-initdb.d/

EXPOSE 5432