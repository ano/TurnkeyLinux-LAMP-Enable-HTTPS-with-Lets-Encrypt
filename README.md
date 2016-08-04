# TurnkeyLinux-LAMP-Enable-HTTPS-with-Lets-Encrypt
Install and Enable HTTPS with Lets Encrypt on TurnkeyLinux LAMP 

###update pip

```
  apt-get remove python-pip
  wget https://bootstrap.pypa.io/get-pip.py
  python get-pip.py
  pip install python2-pythondialog
```

###add backports to Jessie
```
  echo 'deb http://http.debian.net/debian jessie-backports main' > /etc/apt/sources.list.d/jessie-backports.list
  apt-get update
```


###install lets encrypt
```
  apt-get install python-certbot-apache -t jessie-backports
  certbot --apache
```

###configure your apache virtualhosts file
> nano /etc/apache2/sites-available/default-ssl.conf

```
<VirtualHost *:443>
        SSLEngine on
        SSLCertificateFile /etc/letsencrypt/live/licensing.tklapp.com/cert.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/licensing.tklapp.com/privkey.pem 
        SSLCertificateChainFile /etc/letsencrypt/live/licensing.tklapp.com/fullchain.pem
        ServerAdmin licensing@gmail.com
        DocumentRoot /var/www/
</VirtualHost>
```
###(Optional) Force Apache to always use https
```
<VirtualHost *:80>
        ServerAdmin licensing@gmail.com
        DocumentRoot /var/www/
        
        RewriteEngine On
        RewriteCond %{HTTPS} off
        RewriteRule (.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>
```
###restart apache
```
  /etc/init.d/apache2 restart
```
