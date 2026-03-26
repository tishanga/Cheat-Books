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
### download zammad docker folder
```
git clone https://github.com/zammad/zammad-docker-compose.git
```
### up the container
```
ls
cd zammad-docker-compose
docker compose up -d
```
```  
docker ps

```
### navigate to
```
http\\:http://localhost:8080/
```
keep in minds its HTTP not HTTPS
the machine needs to be atleast 4gb ram and 2cores

---
Intial web page will look like this <br>
click setup a new system and give your admin credentiols

 
<img width="556" height="482" alt="image" src="https://github.com/user-attachments/assets/34683300-858a-4636-9089-dce0c77035d0" />


Add the neccsary details here and click  next.


<img width="445" height="613" alt="image" src="https://github.com/user-attachments/assets/4096f412-ba51-4d21-9ad1-a0cb0ee27c47" />


choose smtp and configure your smtp setting typicaly
## ADD the email that your are planing to send the mails through 


<img width="586" height="662" alt="image" src="https://github.com/user-attachments/assets/55af24fb-4cd5-4a9d-86f3-2ce2efd8b1f9" />


## for password copy and paste the app password not the your mail password.


<img width="418" height="603" alt="image" src="https://github.com/user-attachments/assets/1323f171-a28b-4a2b-818c-04ddc3c49e6d" />


### you can skip this part for now


<img width="461" height="503" alt="image" src="https://github.com/user-attachments/assets/e499becd-ed45-4caf-ac1e-c47c4adabab1" />


### navigate to settings > Groups

<img width="1350" height="632" alt="image" src="https://github.com/user-attachments/assets/deb96299-6aff-4dc7-a6d3-53cffb500a01" />

#### create a new group

<img width="341" height="527" alt="image" src="https://github.com/user-attachments/assets/7d6f0581-0ebe-4059-92a5-093898637e3f" />



### navigate to channels > email 
<img width="1247" height="632" alt="image" src="https://github.com/user-attachments/assets/4a8bcaa9-3b0f-43b7-a71c-9f134bb56ddb" />


#### create a new email channel click the expert option
<img width="463" height="600" alt="image" src="https://github.com/user-attachments/assets/bebb5d90-7ac5-47ca-b55c-0b51ebb70247" />

### add the details the

host
```
imap.gmail.com
```
port
```
587
```
#### use the app password
#### add your Gmail acoount and app password you created

<img width="228" height="583" alt="image" src="https://github.com/user-attachments/assets/6832e1c4-4fc9-4f22-9e96-1443e7199624" />

<img width="408" height="397" alt="image" src="https://github.com/user-attachments/assets/3f6df4fb-1701-4063-9989-cbcb7f09490d" />

<img width="408" height="540" alt="image" src="https://github.com/user-attachments/assets/25114a57-6ab6-4ee5-b540-c791c401fd82" />

<img width="1335" height="616" alt="image" src="https://github.com/user-attachments/assets/b891b387-93bc-49c2-b128-d46d58fa0665" />

<img width="1136" height="402" alt="image" src="https://github.com/user-attachments/assets/9c05dc04-02c9-49f4-b63c-a9d92822b73c" />

<img width="1146" height="602" alt="image" src="https://github.com/user-attachments/assets/7768b136-7fed-4b74-850b-020cdda6b5c0" />

<img width="1143" height="596" alt="image" src="https://github.com/user-attachments/assets/411e3e8d-d02e-4632-b0fa-c9c4358aaab4" />

<img width="1137" height="590" alt="image" src="https://github.com/user-attachments/assets/3e0cac5e-0d0b-4504-8a2d-9fb85f2e26d4" />

First Name
Last Name
Email
Password 
Roles - Agent
Group - Helpdesk - Full
Submit

<img width="1142" height="610" alt="image" src="https://github.com/user-attachments/assets/0b15d2e7-530e-4d03-b14e-ae0f2edc2137" />

First Name
Last Name
Email
Password 
Roles - Helpdesk
Group - Helpdesk - Full
Submit

<img width="1146" height="531" alt="image" src="https://github.com/user-attachments/assets/74ad15e4-8b6c-4afe-8686-412227d290db" />
Name - My Assigned Tickets:-
##Available for the following roles * -
Admin
Agent
##Conditions for shown tickets * (select)

##Attributes * -
#
Title
Customer
Group
Created at
Submit

<img width="1140" height="437" alt="image" src="https://github.com/user-attachments/assets/39973401-ad94-4d41-bd28-3f5f7ce02d93" />

Name - Unassigned & Open Tickets :-
##Available for the following roles * -
Admin
Helpdesk
##Conditions for shown tickets * (select)

##Attributes * -
#
Title
Customer
Group
Created at
Submit

<img width="1140" height="577" alt="image" src="https://github.com/user-attachments/assets/b783dc81-637e-4f3c-a1c6-a0561255f18d" />

Name - My Pending Reached Tickets
##Available for the following roles * -
Admin
Agent
##Conditions for shown tickets * (select)
pending close
pending reminder
##Attributes * -
#
Title
Customer
Group
Pending till
Created at
Submit

<img width="1132" height="420" alt="image" src="https://github.com/user-attachments/assets/fd469d5e-029f-4994-af26-9b7cbc21aebe" />

Name - Open Tickets
##Available for the following roles * -
Admin
Helpdesk
##Conditions for shown tickets * (select)
new
open
##Attributes * -
#
Title
Customer
Group
Owner
State
Created at
Submit

<img width="1142" height="432" alt="image" src="https://github.com/user-attachments/assets/584d69e7-9f93-4e0e-9b24-6f814a18599b" />

Name - Pending Reached Tickets
##Available for the following roles * -
Admin
Helpdesk
##Conditions for shown tickets * (select)
pending close
pending reminder
##Attributes * -
#
Title
Customer
Group
Owner
Created at
Submit

<img width="1136" height="365" alt="image" src="https://github.com/user-attachments/assets/c6952e13-458c-44a6-9055-c276f047f995" />

Name - My Replacement Tickets
##Available for the following roles * -
Admin
Agent
##Conditions for shown tickets * (select)
new
open
pending close
pending reminder
##Attributes * -
#
Title
Customer
Group
Owner
Created at
Escalation at
Submit

<img width="1142" height="407" alt="image" src="https://github.com/user-attachments/assets/3fa7664d-9e61-47d8-8859-7bcc87f9dd26" />
Name - Closed Tickets
##Available for the following roles * -
Admin
Helpdesk
##Conditions for shown tickets * (select)
closed
##Attributes * -
#
Title
Customer
Group
Owner
State
Created at
Submit

<img width="1136" height="382" alt="image" src="https://github.com/user-attachments/assets/2eafed71-e673-4e7d-a4f6-753a94ec6f29" />

Name - My Closed Tickets
##Available for the following roles * -
Admin
Helpdesk
##Conditions for shown tickets * (select)
closed
##Attributes * -
#
Title
Customer
Group
Owner
State
Created at
Submit


<img width="1130" height="527" alt="image" src="https://github.com/user-attachments/assets/7002e961-30d5-4895-8f6e-82743793adcf" />

only Active - customer notification (on owner change)

<img width="931" height="532" alt="image" src="https://github.com/user-attachments/assets/6626a29b-c179-43e8-89f3-1ffa6a50b4e2" />

Enable Ticket creation - no - submit

<img width="1145" height="570" alt="image" src="https://github.com/user-attachments/assets/907ec5aa-b212-4413-91fd-aa75023b9c57" />

Name - ALL
Filter
 State - all
Available for the following roles - Admin
Submit

<img width="1132" height="527" alt="image" src="https://github.com/user-attachments/assets/ef6471ba-b486-47de-be32-a8a2100972a7" />

Name
Filter
 State - all
 Owner - Specific user

Available for the following roles - Admin
Submit

docker exec -it zammad-docker-compose-zammad-railsserver-1 /bin/bash

####################
cd ~
####################
cd /opt/zammad
#####
ls bin
##########
bin/rails c
####################
🧠 Even safer (limit test)

Before deleting, see how many will be removed:

Ticket.joins(:state).where(ticket_states: { name: 'new' }).count
#Delete-ALL
Ticket.joins(:state).where(ticket_states: { name: 'new' }).destroy_all

#Delete-Last-1-Hour
Ticket.where('created_at > ?', 1.hour.ago).destroy_all

#Delete only a few first (10):
Ticket.joins(:state).where(ticket_states: { name: 'new' }).limit(10).destroy_all

💡 Optional: delete only older new tickets
Example: older than 30 days

Ticket.joins(:state)
      .where(ticket_states: { name: 'new' })
      .where('tickets.updated_at < ?', 30.days.ago)
      .destroy_all


