# Squid Docker Image 

This *Squid Docker Image* is based on **Alpine Linux**.

## Supported tags and respective `Dockerfile` links

- [`5.2-r0`, `latest`](https://github.com/dmachard/squid-docker/tree/main/5.2)
- [`5.1-r0`](https://github.com/dmachard/squid-docker/tree/main/5.1)
- [`5.0.7-r0`](https://github.com/dmachard/squid-docker/tree/main/5.0.7)
- [`4.17-r0`](https://github.com/dmachard/squid-docker/tree/main/4.17)

## How to use this image

Run this container with the following command:

```
sudo docker run --name squid01 -d -p 3128:3128/tcp --restart=always dmachard/squid:latest
```

Testing squid container

```
$ export http_proxy=127.0.0.1:3128
$ export https_proxy=127.0.0.1:3128

$ wget http://example.com
--2021-10-13 15:59:51--  http://example.com/
Connecting to 127.0.0.1:3128... connected.
Proxy request sent, awaiting response... 200 OK
Length: 1256 (1.2K) [text/html]
Saving to: ‘index.html
```

## Custom configuration

You can run this image and provide your own squid configuration like that:

```
sudo docker run --name squid01 -d -p 3128:3128/tcp -v $PWD/mysquid.conf:/opt/squid/etc/squid.conf \
dmachard/squid:latest
```

## Volume for access Logs

Example to get access logs in your host

```
sudo docker run --name squid01 -d -p 3128:3128/tcp -v $PWD/cache/:/opt/squid/var/logs/ \
dmachard/squid:latest
```