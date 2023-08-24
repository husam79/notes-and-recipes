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

**NOTE:** I advise to reboot the server at this point.

<br/>

## A guide to how to install the Nginx Proxy Manager

https://nginxproxymanager.com/guide/#hosting-your-home-network


