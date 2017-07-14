# OntoBrowser-Docker
Dockorized [OntoBrowser](https://github.com/Novartis/ontobrowser)

# Deployment
```sh
> docker-compose up --build -d
```

After starting the containers, the webapplication is running at http://localhost:8080/ontobrowser

# Upload Example OBO FIle
```sh
> curl -s -S -O -L http://purl.obolibrary.org/obo/ma.obo
> curl -s -S -H "Content-Type: application/obo;charset=utf-8" -X PUT --data-binary "@ma.obo" -u SYSTEM "http://localhost:8080/ontobrowser/ontologies/Mouse%20adult%20gross%20anatomy"
```

# Notes
There is no authentification for uploading OBO files, so please don't use the frontend Docker image in productive environments.
If you want to enable authentification, edit die Dockerfile in the frontend folder and remove `sed -i 's/return username/return "SYSTEM"/g' src/main/java/com/novartis/pcs/ontology/rest/servlet/OntologiesServlet.java`
