#### Monarch Plater

Contains the open api conf and Dockerfile specific to building https://trapi.monarchinitiative.org


.env can be found in monarch configs but looks something like
```
WEB_HOST=0.0.0.0
WEB_PORT=8000
NEO4J_HOST=scigraph.ncats.io
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=<NEO4J-PASSWORD>
NEO4J_HTTP_PORT=80
PLATER_TITLE='Plater'
PLATER_VERSION='1.1.0'
BL_VERSION=2.1.0
```

Build, push to DockerHub, and deploy
```
docker build --tag plater-dev .
docker tag plater-dev monarchinitiative/plater-sri:latest
docker push monarchinitiative/plater-sri:latest

# On the OSU Monarch servers map to port 9000, otherwise 80 or 443
docker run -d --name plater -p 9000:8000 monarchinitiative/plater-sri:latest

# TODO move this to google cloud and add instructions
```

#### Building the docker image on GCP and deploying artifact registry

TODO: change from plater-sri:dev to plater-sri:latest

```
docker build --tag plater-dev .
docker tag plater-dev us-central1-docker.pkg.dev/monarch-initiative/monarch-initiative/plater-sri:dev
docker push us-central1-docker.pkg.dev/monarch-initiative/monarch-initiative/plater-sri:dev
```

To push the image to

```
gcloud compute instances update-container monarch-trapi --container-image=us-central1-docker.pkg.dev/monarch-initiative/monarch-initiative/plater-sri:dev
```
