# traefik-template
Traefik template for developing locally

## Setup
Clone the repo locally and change into that directory
docker-compose.yml
```
version: '3'

services:
  traefik:
    image: traefik:v2.0
    command: --api --providers.docker
    ports:
      - 8080:8080
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /traefik.toml:/etc/traefik
  nginx:
    image: nginx:latest
    ports:
      - 80:80
  influxdb:
    image: quay.io/influxdb/influxdb:2.0.0-alpha
    ports:
      - 9999:9999
    labels:
      - "traefik.http.routers.influxdb.rule=Host('influx.localhost')"
- "traefik.entrypoint.influx"
```
## Compose up
Run the command:
`docker-compose up` to watch the logs 
or
`docker-compose up -d` for it to run in the background. 

## Services
1. The dashboard is running at http://localhost:8080 but it is still under construction in v2.0 but you can view the api info at http://localhost:8080/api/rawdata
2. Nginx is running on the main domain http://localhost
3. InfluxDB 2.0 is running on http://influx.localhost which it should automatically pull up port 9999

## Template
This is a template where anyone can build upon this.  The next step is to configure ssl. (More to come)
