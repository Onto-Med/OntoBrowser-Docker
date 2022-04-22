# OntoBrowser-Docker
Dockerized [OntoBrowser](https://github.com/Novartis/ontobrowser)

# Deployment
Create `docker-compose.env` with PostgreSQL credentials (see `docker-compose.env.tpl`).

```sh
cp docker-compose.env.tpl docker-compose.env
docker-compose up --build -d
```

After starting the containers, the web application is running at http://localhost:8080/ontobrowser

## Connect to an existing PostgreSQL DB
In case you already have a running database, you can modify the environment variables `POSTGRES_HOST`, `POSTGRES_DB`, and `POSTGRES_PORT` in `docker-compose.env` accordingly.
The variables default to the values given in `docker-compose.env.tpl`.
You may also need to modify the `pg_hba.conf` file of your PostgreSQL database (see https://www.postgresql.org/docs/current/auth-pg-hba-conf.html).

Use the sql files in the [backend](backend) folder to initialize the database.

It may be reasonable to strike the unused backend service from the `docker-compose.yml` file.

# Upload Example OBO File
```sh
curl -s -S -O -L http://purl.obolibrary.org/obo/ma.obo
curl -s -S -H "Content-Type: application/obo;charset=utf-8" -X PUT --data-binary "@ma.obo" -u SYSTEM "http://localhost:8080/ontobrowser/ontologies/Mouse%20adult%20gross%20anatomy"
```

# Notes
There is no authentication for uploading OBO files, so please don't use the frontend Docker image in productive environments.
If you want to enable authentication, edit the Dockerfile in the frontend folder and remove `sed -i 's/return username/return "SYSTEM"/g' src/main/java/com/novartis/pcs/ontology/rest/servlet/OntologiesServlet.java`
