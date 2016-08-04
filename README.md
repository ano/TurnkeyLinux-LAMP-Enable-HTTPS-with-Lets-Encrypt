# TurnkeyLinux-LAMP-Enable-HTTPS-with-Lets-Encrypt
Install and Enable HTTPS with Lets Encrypt on TurnkeyLinux LAMP 

#update pip

```
  apt-get remove python-pip
  wget https://bootstrap.pypa.io/get-pip.py
  python get-pip.py
  pip install python2-pythondialog
```

#add backports to Jessie
```
  echo 'deb http://http.debian.net/debian jessie-backports main' > /etc/apt/sources.list.d/jessie-backports.list
  apt-get update
```


#install lets encrypt
```
  apt-get install python-certbot-apache -t jessie-backports
  certbot --apache
```

#configure your apache VirtualHost
```
<VirtualHost 192.168.0.1:443>
  DocumentRoot /var/www/
  ServerName $domain
  SSLEngine on
  SSLCertificateFile /etc/letsencrypt/live/$domain/cert.pem
  SSLCertificateKeyFile /etc/letsencrypt/live/$domain/privkey.pem 
  SSLCertificateChainFile /etc/letsencrypt/live/$domain/fullchain.pem
</VirtualHost> 
```
#restart apache
```
  /etc/init.d/apache2 restart
```
