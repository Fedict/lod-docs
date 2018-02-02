# Docker containers

## Proxy

The [Nginx-proxy](https://github.com/jwilder/nginx-proxy) docker is used to send the requests to the Dropwizard microservices.
The container is set to automatically restart when it exits unexpectedly.

Inside the container, the home directory `/etc/nginx/vhost.d` is used to store persistent vhost-specific configuration data 
as a docker volume, mapped/mounted to the host file system `/home/opendata/data/nginx/vhost.d`. 
This directory must be readable for the container.
```
docker run --name nginx --restart=unless-stopped -d -p 80:80 -p 443:443 -v /home/opendata/certs/:/etc/nginx/certs -v /var/run/docker.sock:/tmp/docker.sock:ro -v /home/opendata/data/nginx/vhost.d:/etc/nginx/vhost.d jwilder/nginx-proxy:alpine 
```

To allow browser-based tools like the visualization tool, one should add CORS-headers to the responses of the various LOD containers. 
This can be done by adding these HTTP headers in the `default` nginx vhost configuration, e.g. 
```
add_header 'Access-Control-Allow-Origin' '*' ;
add_header 'Access-Control-Allow-Methods' 'GET, OPTIONS' ;
```

## RDF Triple Store

This can be a [GraphDB](GRAPHDB.md) triple store, or another store supporting [RDF4j](http://rdf4j.org/).
In this example the default GrapHDB workbench port (7200) is mapped to the host port 8443

```
docker run --restart=unless-stopped --name graphdb7 -p 8443:7200 -d -v /home/opendata/data/graphdb:/home/graphdb/data ontotext/graphdb
```
