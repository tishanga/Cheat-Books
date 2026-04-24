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
## certbot

```
sudo apt install certbot python3-certbot-apache -y
```
 Verify Apache Virtual Hosts
Koha creates two interfaces — OPAC (public) and Staff (admin). Check your current vhosts:
bash# List enabled sites
```
ls /etc/apache2/sites-enabled/
```

View Koha's Apache config (replace LIBRARYNAME with your instance name)
```
cat /etc/apache2/sites-enabled/library.conf
```
Ensure Both Sites Have ServerName
Each virtual host must have a ServerName directive for Certbot to work. Edit if needed:
```
sudo nano /etc/apache2/sites-enabled/LIBRARYNAME.conf
```

Obtain SSL Certificates
Option A — Let Certbot auto-configure Apache (recommended):
bash# For OPAC
```
sudo certbot --apache -d opac.yourdomain.com
```
For Staff interface
```
sudo certbot --apache -d staff.yourdomain.com
```
Option B — Get certificate only, configure manually:
```
sudo certbot certonly --apache -d opac.yourdomain.com -d staff.yourdomain.com
```

Update Koha's Apache Config for Staff SSL
The Staff interface often runs on port 8080. You need to make it listen on 443 (or a custom SSL port). Edit your Koha config:
```
sudo nano /etc/apache2/sites-enabled/library.conf
```

Enable SSL Module & Update Ports
bash# Enable SSL module
```
sudo a2enmod ssl
```
Enable headers module (needed for HSTS)
```
sudo a2enmod headers
```
Make sure Apache listens on 443
```
sudo nano /etc/apache2/ports.conf
```
Ensure ports.conf contains:
apache

`Listen 80
Listen 443

<IfModule mod_ssl.c>
    Listen 443
</IfModule>`


Update Koha System Preferences
After SSL is working, update Koha's internal URLs:

Log in to Staff interface
Go to Administration → System Preferences
Search for and update:

OPACBaseURL → https://opac.yourdomain.com
staffClientBaseURL → https://staff.yourdomain.com

Test and Reload Apache
bash# Test Apache config for errors
```
sudo apache2ctl configtest
```
If output is "Syntax OK", reload
```
sudo systemctl reload apache2
```
Step 9: Verify Auto-Renewal
Certbot sets up a systemd timer for auto-renewal. Verify it:
bash# Check renewal timer
```
sudo systemctl status certbot.timer
```
Test renewal (dry run)
```
sudo certbot renew --dry-run
```


Troubleshooting Tips
IssueFixPort 80 blockedOpen it: sudo ufw allow 80 and sudo ufw allow 
443Domain not resolvingVerify DNS A record points to your server 
IPCertificate not issuedCheck sudo journalctl -xe for errorsStaff on port 8080
Update VirtualHost from *:8080 to *:443 with SSL directivesMixed content warnings
Ensure all Koha URLs use https:// in System Preferences

## logs delete

Identify What's Taking Up Space
bash# Overall disk usage
```
df -h
```
Find the biggest directories from root
```
sudo du -h --max-depth=2 / 2>/dev/null | sort -rh | head -30
```
Check Koha-specific directories
```
sudo du -sh /var/log/koha/*
sudo du -sh /var/lib/mysql/
sudo du -sh /usr/share/koha/
sudo du -sh /var/spool/
```
Step 2: Clean Up Koha Logs
Locate Koha Logs
bash# Koha instance logs (replace LIBRARYNAME)
```
ls -lh /var/log/koha/LIBRARYNAME/
```
Common log files
```
sudo du -sh /var/log/koha/LIBRARYNAME/*.log
```


Manually Clear Old Logs
bash# Truncate (empty) logs without deleting the file
sudo truncate -s 0 /var/log/koha/LIBRARYNAME/plack-error.log
sudo truncate -s 0 /var/log/koha/LIBRARYNAME/plack-access.log
sudo truncate -s 0 /var/log/koha/LIBRARYNAME/opac-error.log
sudo truncate -s 0 /var/log/koha/LIBRARYNAME/intranet-error.log

#### Delete rotated/compressed old logs
sudo find /var/log/koha/ -name "*.gz" -delete
sudo find /var/log/koha/ -name "*.1" -delete
sudo find /var/log/apache2/ -name "*.gz" -delete
Configure Logrotate for Koha (prevent future bloat)
bashsudo nano /etc/logrotate.d/koha
Paste this:
/var/log/koha/*/*.log {
    daily
    missingok
    rotate 7
    compress
    delaycompress
    notifempty
    sharedscripts
    postrotate
        systemctl reload apache2 > /dev/null 2>&1 || true
    endscript
}

Step 3: Clean Up System Logs
bash# Clean systemd journal logs (keep only last 3 days)
sudo journalctl --vacuum-time=3d

Or limit by size (keep only 200MB)
sudo journalctl --vacuum-size=200M

Check size before/after
sudo journalctl --disk-usage

Clean Apache logs
sudo find /var/log/apache2/ -name "*.gz" -delete
sudo find /var/log/apache2/ -name "*.log.*" -delete

Step 4: Clean Up MySQL / MariaDB (Koha Database)
bash# Check database size
sudo mysql -e "SELECT table_schema AS 'Database', 
ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS 'Size (MB)' 
FROM information_schema.tables GROUP BY table_schema;"

Check binary logs (these can be huge)
sudo mysql -e "SHOW BINARY LOGS;"

Purge binary logs older than 7 days
sudo mysql -e "PURGE BINARY LOGS BEFORE DATE(NOW() - INTERVAL 7 DAY);"

Check and disable binary logging if not needed for replication
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
Add or uncomment: skip-log-bin

Step 5: Clean Koha's Internal Action Logs (Database)
Koha stores action logs inside the database which can grow huge:

Go to Staff Interface
Administration → System Preferences → Logs
Disable logging for noisy events you don't need

Then purge old logs via the database:
bashsudo koha-mysql LIBRARYNAME
sql-- Check log table size
SELECT COUNT(*) FROM action_logs;

-- Delete logs older than 6 months
DELETE FROM action_logs WHERE timestamp < DATE_SUB(NOW(), INTERVAL 6 MONTH);

-- Reclaim disk space
OPTIMIZE TABLE action_logs;

EXIT;

Step 6: Transfer Logs to Another Location
Option A — Copy to External Drive / NAS
bash# Mount external drive first
```
sudo mount /dev/sdb1 /mnt/backup
```
Archive and move logs
```
sudo tar -czf /mnt/backup/koha-logs-$(date +%Y%m%d).tar.gz /var/log/koha/
sudo tar -czf /mnt/backup/apache-logs-$(date +%Y%m%d).tar.gz /var/log/apache2/
```
After verifying archive, clear originals
```
sudo find /var/log/koha/ -name "*.log" -exec truncate -s 0 {} \;
```
Option B — Transfer to Remote Server via SCP

bash# Send logs to remote server
```
scp -r /var/log/koha/ user@remote-server:/backup/koha-logs/
```
Or use rsync (faster for large files)
```
rsync -avz /var/log/koha/ user@remote-server:/backup/koha-logs/
```
Option C — Automate with a Cron Job
bash
```
sudo crontab -e
```
Add:
bash# Every Sunday at 2am — archive and clear logs older than 30 days
```
0 2 * * 0 tar -czf /mnt/backup/koha-logs-$(date +\%Y\%m\%d).tar.gz /var/log/koha/ && find /var/log/koha/ -name "*.gz" -delete
```
Step 7: General System Cleanup
bash# Remove unused packages and cache
```
sudo apt autoremove -y
sudo apt clean
sudo apt autoclean
```
Clear thumbnail/temp cache
```
sudo rm -rf /tmp/*
sudo rm -rf /var/tmp/*
```
Find large files over 100MB anywhere
```
sudo find / -type f -size +100M 2>/dev/null | sort -k5 -rh
```



expand disk space

Step 1: Extend disk in your hypervisor (VMware/VirtualBox/Proxmox) first
Then in Linux:

Check current partitions
```
lsblk
sudo fdisk -l
```
If using LVM (most Ubuntu/Debian servers do)
```
sudo pvdisplay
sudo vgdisplay
sudo lvdisplay
```
Extend the logical volume (replace with your actual LV path)
```
sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```
Resize the filesystem
```
sudo resize2fs /dev/ubuntu-vg/ubuntu-lv
```

# ssh key gen 
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
# Verify
```
df -h
```
