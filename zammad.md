# Zammad documentation

## Comman Dashboard

once you logged in your inital dashboard will look like this

##Help Desk Dashboard
help desk dashboard 

### only for the first time docker compose installation
```
sudo apt update && sudo apt install -y nano iputils-ping curl traceroute nginx net-tools htop nmap tcpdump wget unzip git vim ufw dnsutils
apt install docker.io
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
download zammad docker folder
```
git clone https://github.com/zammad/zammad-docker-compose.git
```
up the container
```
ls
cd zammad-docker-compose
docker compose up -d
```
```  
docker ps
```
