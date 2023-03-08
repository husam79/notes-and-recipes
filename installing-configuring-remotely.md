# Installing and configuring the Remotely application

## Creating a VM
You can use any cloud (or local) host to create suitable VM with good specifications (especially in CPU power).
- You should allow inbound connection on ports 80, 81 and 443
- Make sure that the external ip address is a static ip address.

## Installing Docker and Docker-Compose
Use the following shell script to install them
```
#!/bin/bash

sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -m 0755 -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin



sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

<br/>

## Adding the current user to the docker group
This step is optional but it is recommended is case you don't want to use the command sudo whenever you use the docker command. Use the following command to add the user "husam" to the group "docker":
```
sudo usermod -aG docker husam
```

<br/>

## Using the docker compose to build the environment
- The following script will create three container (in one virtual network): 
    - Nginx proxy manager. 
    - Mariadb database server (required by Nginx proxy manager).
    - Remotely app. 
- Please **change critical information like passwords to be more complicated**.

- Copy the content of the following code to a file with the name: **docker-compose.yml**
```
version: "3"
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80' # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81' # Admin Web Port
      # Add any other Stream port you want to expose
      # - '21:21' # FTP
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "npm"
      DB_MYSQL_PASSWORD: "npm"
      DB_MYSQL_NAME: "npm"
      # Uncomment this if IPv6 is not enabled on your host
      DISABLE_IPV6: 'true'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
    depends_on:
      - db

  db:
    image: 'jc21/mariadb-aria:latest'
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: 'npm'
      MYSQL_DATABASE: 'npm'
      MYSQL_USER: 'npm'
      MYSQL_PASSWORD: 'npm'
    volumes:
      - ./data/mysql:/var/lib/mysql

  remotely:
    image: immybot/remotely
    restart: unless-stopped
    ports:
      - '5000:5000'
    volumes:
      - /var/www/remotely:/remotely-data
```

Use the following command to build the environment (**pay attention to run this command in the same folder as the docker-compose.yml file exist**):
```
docker-compose up -d
```

<br/>

**NOTE:** I advice to reboot the server at this point.
