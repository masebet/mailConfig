apt update 
apt upgrade
apt install sudo
adduser {username}
sudo passwd {username}
adduser {username} sudo
sudo hostnamectl set-hostname arindana.com

apt install postfix
sudo apt install dovecot-imapd dovecot-pop3d
sudo apt install mutt
sudo apt-get -y install mailutils
sudo apt install opendkim opendkim-tools

sudo nano /etc/dovecot/dovecot.conf
	listen = *, ::
sudo nano /etc/dovecot/conf.d/10-auth.conf
	disable_plaintext_auth = no
	auth_mechanisms = plain login
sudo nano /etc/dovecot/conf.d/10-mail.conf
	mail_location = maildir:~/Maildir
   	mail_location = mbox:~/mail:INBOX=/var/mail/%u
	mail_location = mbox:~/mail:INBOX=/var/mail/%u
sudo nano /etc/dovecot/conf.d/10-master.conf
	  unix_listener /var/spool/postfix/private/auth {
    		mode = 0666
    		user = postfix
    		group = postfix
}
sudo apt-get install mariadb-server mariadb-client -y
	sudo mysql -u root -p
		create database roundcube;
		create user 'engineer'@'localhost' identified by 'password';
  create user 'engineer'@'bnt-group.co.id' identified by 'kakacinta';
		grant all privileges on roundcube.* to 'engineer'@'bnt-group.co.id';
		flush privileges;

sudo apt install roundcube
nano /etc/roundcube/config.inc.php
	$config[‘default_host’] = 'arindana.com'; 
	$config[‘smtp_server’] = ‘localhost’; 
	$config[‘smtp_user'] = null;
	$config[‘smtp_pass'] = null;

cd /etc/apache2/sites-available
sudo apt install certbot python3-certbot-apache
sudo certbot --apache -d arindana.com -d www.arindana.com
   /etc/letsencrypt/live/arindana.com/fullchain.pem
   /etc/letsencrypt/live/arindana.com/privkey.pem
sudo certbot renew --dry-run

cp 000-default.conf mail.conf
nano mail.conf
	ServerName arindana.com
	DocumentRoot /var/lib/roundcube
a2ensite mail.conf
systemctl reload apache2

echo "Ini adalah body email" | mail -s "Hello world" info@mail.com
mutt -f imaps://karebet@arindana.com

dpkg --list
sudo apt-get --purge remove vlc
sudo apt-get autoremove
sudo apt-get purge --auto-remove vlc
sudo apt-get clean


scp -r pocoBnt ssh root@103.190.28.108:/root
scp -r pocoBnt ssh root@arindana.com:/root


POCO ===================================================================

sudo nc -nvlp 777
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf > /dev/null
apt update -y
apt install build-essential
apt install libpoco-dev
apt install git
apt install nodejs npm

git clone https://github.com/masebet/pocoBnt.git
git clone https://github.com/masebet/chatApp.git

touch /etc/systemd/system/http.service
nano /etc/systemd/system/http.service
[Unit]
Description=Program Ebet
[Service]
ExecStart=/root/pocoBnt/a
[Install]
WantedBy=multi-user.target

touch /etc/systemd/system/chat.service
nano /etc/systemd/system/chat.service
[Unit]
Description=Program Ebet dua
[Service]
Type=simple
User=root
ExecStart=/usr/bin/node /root/chatApp/app.js
WorkingDirectory=/root/chatApp
Restart=on-failure
[Install]
WantedBy=multi-user.target

systemctl daemon-reload
systemctl enable http.service
systemctl enable chat.service

string a = "/root/pocoBnt"+request.getURI();
if(a=="/root/pocoBnt/")a="/root/pocoBnt/index.html";
reboot
===========================================================POCO

pm uninstall -k --user 0 com.google.android.youtube
