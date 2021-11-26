
# Install and Setup Vtiger CRM on Ubuntu
## Install LAMP Stack

### Step-1==> Setup apache2

sudo apt update     
sudo apt install -y apache2 apache2-utils    
sudo systemctl status apache2      
sudo systemctl start apache2  
sudo systemctl enable --now apache2      
sudo systemctl restart apache2      

## Step-2==> ufw install  

```
sudo apt install ufw          
sudo ufw status          
sudo ufw logging on      
sudo ufw enable          
sudo systemctl restart ufw         

sudo ufw allow 22/tcp    
sudo ufw allow 80/tcp     
sudo ufw allow 443/tcp  

sudo systemctl restart ufw   

```


### Step 3: Enabling HTTPS
#### FOR Apache : 
-----------------------------

```
sudo apt install certbot -y   
sudo apt install python3-certbot-apache -y    
sudo certbot --apache --agree-tos --redirect --hsts --staple-ocsp --email admin@domain.com -d dmain.com   
```
     
## Step-4==> Setup MariaDB 

```
sudo apt install mariadb-server mariadb-client          
sudo systemctl status mariadb      
sudo systemctl start mariadb       
sudo systemctl enable mariadb      
sudo systemctl restart mariadb 

sudo mysql_secure_installation

```
## Step-5==> Create Database and Database


```

sudo mysql -u root -p         
create database vtiger default character set utf8 default collate utf8_general_ci;        
create user vtigeradmin@localhost identified by '@Ausa4422';          
grant all on vtiger.* to vtigeradmin@localhost;        
flush privileges;        
exit      
```

```
echo -e '[mysqld]\nsql_mode = ""' >> /etc/mysql/my.cnf          
sudo systemctl restart mysql   

```

```
DB_HOST=localhost 
DATABASE_NAME=vtigeradmin 
DB_Password=@Ausa4422 
DB_USER=vtiger

```

## Step-6==> Install PHP 7.4

``````
sudo apt install software-properties-common       
sudo add-apt-repository ppa:ondrej/php       
sudo apt update          

apt install php7.4 php-imap php-curl php-xml php-mysql php-mbstring php-bcmath php-gd php-soap -y

sudo apt install php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl -y                 

php -v    
```
### Step-7==> Configure PHP for Vtiger
### Open the /etc/php/7.4/apache2/php.ini configuration file and make the following adjustments;
##### (if php7.4 versone)


```
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


### Step-8==> download vtiger vtigercrm7.3.0 or vtigercrm7.4.0

```
cd /var/www    
sudo wget https://jaist.dl.sourceforge.net/project/vtigercrm/vtiger%20CRM%207.3.0/Core%20Product/vtigercrm7.3.0.tar.gz   
sudo wget https://altushost-swe.dl.sourceforge.net/project/vtigercrm/vtiger%20CRM%207.4.0/Core%20Product/vtigercrm7.4.0.tar.gz
sudo mkdir /var/www/vtigercrm      
sudo tar xzf vtigercrm7.3.0.tar.gz --strip-components=1 -C /var/www/vtigercrm/  
sudo rm vtigercrm7.3.0.tar         
```
## Step-9==> setup config file

```

sudo vim /etc/apache2/sites-available/vtigercrm.conf

   
     <VirtualHost *:80>       
     ServerName domain.com    
     DocumentRoot /var/www/vtigercrm/   
     
     <Directory /var/www/vtigercrm/>    
        Options FollowSymlinks     
        AllowOverride All     
        Require all granted   
     </Directory>   

     ErrorLog /var/log/apache2/vtigercrm_error.log     
     CustomLog /var/log/apache2/vtigercrm_access.log combined    
     </VirtualHost>

```

###  Step-10==> 

```
sudo chown -R www-data:www-data /var/www/vtigercrm/    
sudo a2dissite 000-default.conf    
sudo a2enmod rewrite     
sudo a2ensite vtigercrm.conf  
sudo systemctl restart apache2     
sudo ufw allow 80/tcp         
```

###### You can then access it via the address, http://server-IP-or-hostname.On the welcome page, click Install button to go through the setup wizard.and follow me config   done!!!!!!       



``````   
sudo systemctl restart apache2          
sudo systemctl restart mysql   

```



