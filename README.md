# traefik-template
Traefik template for developing locally

## Setup
Clone the repo locally and change into /traefik-template  
Here is what the docker-compose file looks like.  
```
version: '3'

services:
  traefik:
    image: traefik:v1.7
    command: --api --docker
    ports:
      - 8080:8080
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
  nginx:
    image: nginx:latest
    ports:
      - 80:80
  influxdb:
    image: quay.io/influxdb/influxdb:2.0.0-alpha
    ports:
      - 9999:9999
```
## Traefik.toml
```
[docker]
endpoint = "unix:///var/run/docker.sock"
domain = "localhost"
watch = true
exposedByDefault = true
usebindportip = true
swarmMode = false
network = "web"
[api]
dashboard = true
entryPoint = "traefik"
debug = true
```
This configuration is a basic setup to expose the dashboard.  
Check it out.  

## Compose up
Run the command:
`docker-compose up` to watch the logs 
or
`docker-compose up -d` for it to run in the background. 

## Services
1. The dashboard is running at http://localhost:8080 
2. Nginx is running on the main domain http://localhost
3. InfluxDB 2.0 is running on http://influx.localhost:9999 which it should automatically pull up port 9999

## Template
This is a template where anyone can build upon this.  The next step is to configure ssl. (More to come)
