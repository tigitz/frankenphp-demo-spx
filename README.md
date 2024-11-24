# FrankenPHP & SPX integration

This repository provides a Docker-based infrastructure which can help to reproduce or debug issues related to the integration of FrankenPHP in worker mode with SPX.

### The project

Run the project with Docker (worker mode):

```console
docker run --rm -it -v $PWD:/app composer:latest install && \
docker build -t frankenphp-spx . && \
docker run --rm -it -v $PWD:/app frankenphp-spx bin/console d:m:m --no-interaction && \
docker run --rm \
    -e FRANKENPHP_CONFIG="worker ./public/index.php" \
    -v $PWD:/app \
    -p 80:80 -p 443:443/tcp -p 443:443/udp \
    --name FrankenPHP-demo \
    frankenphp-spx
```

Then you cannot access to SPX's web UI here https://localhost:8500/?SPX_KEY=dev&SPX_UI_URI=/

In non worker mode it works:

```console
docker run --rm -it -v $PWD:/app composer:latest install && \
docker build -t frankenphp-spx . && \
docker run --rm -it -v $PWD:/app frankenphp-spx bin/console d:m:m --no-interaction && \
docker run --rm \
    -v $PWD:/app \
    -p 80:80 -p 443:443/tcp -p 443:443/udp \
    --name FrankenPHP-demo \
    frankenphp-spx
```