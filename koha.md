update and upgrade
```
sudo apt-get update && apt-get upgrade -y
```
add koha repo
```
echo deb http://debian.koha-community.org/koha stable main | sudo tee /etc/apt/sources.list.d/koha.list
wget -O- http://debian.koha-community.org/koha/gpg.asc | sudo apt-key add -
```
update again

install koha
```
sudo apt install koha-common
```

```
sudo apt-get update
sudo apt-get install koha-common
```

edit site conf
```
sudo nano /etc/koha/koha-sites.conf
```
install mysql-server
```
sudo apt install mysql-server
```

apache
```
sudo a2enmod rewrite
sudo a2enmod cgi
sudo systemctl restart apache2
```

koha db
```
sudo koha-create --create-db library
```
edit ports.conf
```
sudo nano etc/apache2/ports.conf
```
restrat apache
```
sudo systemctl restart apache2
```
disable apache defualt
```
sudo a2dissite 000-default
sudo a2enmod deflate
sudo a2ensite library
```

```
sudo koha-passwd library
```

Username for library: koha_library
Password for library: 8mfd=H`{[#Fy0;Je
got localhot:8080

## troubleshoot
#### perl dependencies

check perl version
```
perl-v
```
```
cpan-v
```
```
sudo apt-get install cpanminus
```
```
sudo cpanm GD::Barcode: QRcode
```
or
```
sudo cpan
```
```
install GD: Barcode::QRcode
```
```
perl-MGD::Barcode: QRcode -e 'print "Installed\n";"
```
```
sudo systemctl restart koha-common
```
if still not resolved
```
sudo apt-get install libgd-barcode-perl libgd-perl
```
```
sudo apt-get install libgd-barcode-perl
```
