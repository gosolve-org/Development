# Intro
This repository includes all tools and documentation to set you up to develop on goSolve's services.

# Back-end
## Requirements
Make sure you have these tools installed:
- [Docker](https://www.docker.com/products/docker-desktop/)
- Docker Compose (included in Docker for windows and macos, for linux: [see instructions](https://docker-docs.netlify.app/compose/install/#install-compose))
- [mkcert](https://github.com/FiloSottile/mkcert#installation)

## First time setup
### Install development certificate
To be able to run our services over https, we need to install a development certificate.  
Execute following commands in this directory (the root of this repository):
```shell
# If it's the firt install of mkcert, run
mkcert -install

mkcert -cert-file certs/local-cert.pem -key-file certs/local-key.pem "localhost"
```

## Running an API
**First** run the docker-compose.yml file in this repository.  
This sets up shared dependencies such as Traefik, a database and a redis.
```shell
docker-compose up
```

**The next step** is running the project (or multiple projects at the same time):  
| Method | Description |
| ------ | ----------- |
| Visual Studio (easiest)   | Run the docker-compose project in Visual Studio. (This also enables debugging features.) |
| Terminal | Run `docker-compose up` in a terminal in the project directory. |  

:x: On errors, try removing your /obj and /bin folders. 

### Traefik routing (port 5001 (https) | port 5000 (http))
We use Traefik as the reverse proxy for our local development. This means we can spin up as many services as we want without any port conflicts.  
This causes some URL differences between Azure hosted services and local services:  
Azure: `https://my-api.gosolve.org/api/v1/books`  
Local: `https://localhost:5001/my-api/api/v1/books`
