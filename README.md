# Squid Docker Image 

This **Squid Docker Image** is based on Alpine Linux.

## Supported tags and respective `Dockerfile` links

- [`5.2-r0`, `latest` (*5.2/Dockerfile*)](https://github.com/dmachard/squid-docker/tree/main/5.2)
- [`5.1-r0`, (*5.1/Dockerfile*)](https://github.com/dmachard/squid-docker/tree/main/5.1)
- [`4.17-r0`, (*4.17/Dockerfile*)](https://github.com/dmachard/squid-docker/tree/main/4.17)

## How to use this image

Run this container with the following command:

```
docker run --name squid01 -d -p 3128:3128/tcp --restart=always dmachard/squid:latest
```

## Custom configuration

You can run this image and provide your own squid configuration like that:

```
docker run --name squid01 -d -p 3128:3128/tcp -v $PWD/mysquid.conf:/opt/squid/etc/squid.conf dmachard/squid:latest
```

## Volume for access Logs

Example to get access logs in your host

```
docker run --name squid01 -d -p 3128:3128/tcp -v $PWD/cache/:/opt/squid/var/logs/ dmachard/squid:latest
```