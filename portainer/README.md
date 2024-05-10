# Steps to set up portainer in Ubuntu VM:

#portainer 

this is how i set up portainer on a proxmox ubuntu vm

first install ubuntu VM inside of proxmox 
install vm - ubuntu server
ip address is $ip a
then use solar putty to ssh 
install docker:          

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

then:

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

then to verify: 

sudo docker run hello-world

add user to sudo and docker groups:
$ usermod -aG sudo [username]
$ usermod -aG docker [username]

$ groups
should show you the groups that you are a part of now

install docker compose: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-22-04 

make directory /home/james/homepage/config


install homepage:
useing docker compose:

version: "3.3"
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    environment:
      PUID: 1000 -- optional, your user id
      PGID: 1000 -- optional, your group id
    ports:
      - 3000:3000
    volumes:
      - /path/to/config:/app/config # Make sure your local config directory exists
      - /var/run/docker.sock:/var/run/docker.sock:ro # optional, for docker integrations
    restart: unless-stopped


    find puid and pgid : $ id


install portainer: https://docs.portainer.io/start/install/server/docker/linux 
go to local:9443
user: admin
put in password 2Zt#Lk=/315u6li"yPCz{A4D7FQW0\-@
put in key - look in email
set up envinronment
