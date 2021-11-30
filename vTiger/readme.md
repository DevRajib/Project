
# Install and Setup Vtiger CRM on Ubuntu
## Install LAMP Stack

```
######## Step===> 1

sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update

sudo apt install apache2 apache2-utils mariadb-server mariadb-client php7.4 php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl php-bcmath php-imap php-curl php-xml php-mysql php-mbstring php-bcmath php-gd php-soap -y

sudo systemctl start apache2
sudo systemctl enable --now apache2
sudo systemctl restart apache2

sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl restart mariadb

######## Step===> 2

cd /var/www
sudo mkdir /var/www/vtigercrm

sudo wget https://jaist.dl.sourceforge.net/project/vtigercrm/vtiger%20CRM%207.3.0/Core%20Product/vtigercrm7.3.0.tar.gz
sudo tar xzf vtigercrm7.3.0.tar.gz --strip-components=1 -C /var/www/vtigercrm/

or

sudo wget https://altushost-swe.dl.sourceforge.net/project/vtigercrm/vtiger%20CRM%207.4.0/Core%20Product/vtigercrm7.4.0.tar.gz
sudo tar xzf vtigercrm7.4.0.tar.gz --strip-components=1 -C /var/www/vtigercrm/


######## Step===> 3

sudo vim /etc/apache2/sites-available/vtigercrm.conf

 <VirtualHost *:80>       
 ServerName devopshub.cf
 DocumentRoot /var/www/vtigercrm/   
 
 <Directory /var/www/vtigercrm/>    
    Options FollowSymlinks     
    AllowOverride All     
    Require all granted   
 </Directory>   

 ErrorLog /var/log/apache2/vtigercrm_error.log     
 CustomLog /var/log/apache2/vtigercrm_access.log combined    
 </VirtualHost>

######## Step===> 4
sudo chown -R www-data:www-data /var/www/vtigercrm/
sudo a2dissite 000-default.conf
sudo a2enmod rewrite
sudo a2ensite vtigercrm.conf
sudo systemctl restart apache2
sudo ufw allow 80/tcp

######## Step===> 5 
sudo apt install certbot -y
sudo apt install python3-certbot-apache -y
sudo certbot --apache --agree-tos --redirect --hsts --staple-ocsp --email admin@devopshub.cf -d devopshub.cf

######## Step===> 6

sudo vim /etc/php/7.4/apache2/php.ini  

max_execution_time = 600   
max_input_time = 600               
max_input_vars = 10000  
memory_limit = 1024M   

default_socket_timeout = 600                      
log_errors = Off         
post_max_size = 50M      
upload_max_filesize = 50M           
      
Save it
sudo systemctl restart apache2

```
#############################################################################################################################################


## Step-6==> Create Database and Database

sudo mysql_secure_installation

```
sudo mysql -u root -p         
create database vtiger default character set utf8 default collate utf8_general_ci;        
create user vtigeradmin@localhost identified by '@Ausa4422';          
grant all on vtiger.* to vtigeradmin@localhost;        
flush privileges;        
exit      
```

```
sudo su
echo -e '[mysqld]\nsql_mode = ""' >> /etc/mysql/my.cnf
sudo systemctl restart mysql
exit

```


### This is not commund

```
DB_HOST=localhost 
DATABASE_NAME=vtigeradmin 
DB_Password=@Ausa4422 
DB_USER=vtiger

```


#############################################################################################################################################


#############################################################################################################################################

```
sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
sudo netfilter-persistent save
```

``````   
sudo systemctl restart apache2          
sudo systemctl restart mysql   

```



