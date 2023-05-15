# Docker Commands & Notes
Common Docker's commands and notes

## docker commands
```
docker ps
```
  - displays all running containers.
  - If the parameter **-a** is provided, then it will display all running and stopped containers.
<br/>

```
docker run -d -p [host-port]:[container-port] --name [container-name] [img-name]:[tag]
```
running a container with a specified [img-name]:[tag]
  - -d: detach mode.
  - -p [host-port]:[container-port] link a host port with a container port
  - --name [container-name]: you can optionally specify a name for this container, to refer to it instead of the container id.
  - [img-name]: required, the name of the image like (nginx, ... etc)
  - [tag]: optional, represents the version number of the image, if omitted it will be considered 'latest'
  
<br/>

```
docker start [container-id OR container_name]
```
Starting a previously stopped container with specified id or name.
  
<br/>

```
docker stop [container-id OR container_name]
```
Stopping a running container with specified id or name.

<br/>

```
docker images
```
Displays all available images

<br/>

```
docker logs [container-id OR container-name] -f
```
Displaying logs of the specified container, if the **-f** parameter is provided it will logs in streaming mode

<br/>

```
docker inspect \
  -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' [container_name_or_id]
```
Get the ip address of the [container_name_or_id]

<br />

```
docker rm -f $(docker ps -a -q)
```
Delete all containers.

<br />

```
docker volume rm $(docker volume ls -q)
```
Delete all volumes.

<br />

```
docker stop $(docker ps -aq)
```
Stopping all running containers.

<br />

```
docker rmi $(docker images -q)
```
Removing all images.

<br/>

```
docker network prune
```
This will remove all custom networks not used by at least one container.

<br />

## docker commands
|#|Command|Description|
|---|---|---|
|7|docker exec -it [container-id OR container-name] /bin/bash (OR /bin/sh)| Allows to connect to the specified container as root user |
|||-it: interactive mode|
|8|docker network ls| List all available networks in docker |
|9|docker network create [network-name]| creating a new network named “network-name” |
|10|docker network connect [network-name] [container-name OR container-id] | Assigning a network to an existing container **NOTE:** you can assign a network directly to an container when first run it using the following command: docker run --network [network-name] [image-name]|
|11|docker build -t [new-img-name]:[tag] .| Building a new docker image based on the Dockerfile founded in the currenc directory |

## docker composer commands
|#|Command|Description|
|---|---|---|
|1|docker-compose -f [name-of-yaml-file] up -d|create all services that located in the yaml file in detach mode (it will create a network also)|
|2|docker-compose -f [name-of-yaml-file] down|stop all services that located in the yaml file (including the network also)|

## Notes
- The difference between run and start commands is that: the run command create a new container from an image, whereas the start container runs a previously stopped container.
- Docker images is a set of layers. The lower layer is the operating system layer (normally it is linux alpain because it is lightweight),  and the top most one is the app layer. And there are a number of other layers (service layers).
- All the data in the container will lost, if the container is restarted.

## The internal host address
You can use "host.docker.internal" as internal host address like "localhost but for the machine that host this docker container. You can use this address inside a configuration file for nginx for example to refer to the machine local address.

for example:
http://host.docker.internal:3000 <=> http://localhost:3000 (localhost here is for the hosting machine as I mentioned)

# Nginx Docker Container Configuration
Usefull links: 
- [The server side blog](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Docker-Nginx-reverse-proxy-setup-example)
- [How to Use the NGINX Docker Official Image](https://www.docker.com/blog/how-to-use-the-official-nginx-docker-image/)

## Static files served by the nginx container
This content should be placed in the `/usr/share/nginx/html` in the docker container.

## A sample file for nginx configuration file in a docker container
the following configuration sample supposes that this nginx container communicate with external service (not a docker container) located on the same hosting machine (this is why we use the address: http://host.docker.internal:3000).

**This file is located in `/etc/nginx/conf.d/default.conf` in the docker container.**

```
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
    }
    
    location /api {
        proxy_pass http://host.docker.internal:3000;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}

```
## Restart nginx to make previous changes takes effect
```
sudo docker exec nginx-base nginx -t
sudo docker exec nginx-base nginx -s reload
```
