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
###download zammad docker folder
```
git clone https://github.com/zammad/zammad-docker-compose.git
```
###up the container
```
ls
cd zammad-docker-compose
docker compose up -d
```
```  
docker ps

```
###navigate to
```
http\\:http://localhost:8080/
```
keep in minds its HTTP not HTTPS

the machine needs to be atleast 4gb ram and 2cores

<img width="463" height="553" alt="image" src="https://github.com/user-attachments/assets/b82e9816-9a18-4fd6-8acf-52e9b51b5b62" />

---
Intial web page will look like this
<img width="556" height="482" alt="image" src="https://github.com/user-attachments/assets/34683300-858a-4636-9089-dce0c77035d0" />

