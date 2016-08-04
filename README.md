# TurnkeyLinux-LAMP-Enable-HTTPS-with-Lets-Encrypt
TurnkeyLinux LAMP enable HTTPS with Lets Encrypt

#install lets encrypt (https)
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
