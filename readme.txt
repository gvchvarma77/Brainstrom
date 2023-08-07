installtion of nginx

cmd: sudo apt update

cmd: sudo apt upgrade

cmd:sudo apt install nginx

cmd: sudo ufw allow 'Nginx HTTP'

cmd: sudo ufw allow 'Nginx HTTPS'

cmd: sudo ufw allow 'Open SSH'

cmd: sudo ufw status verbose

Installing MySQL

cmd: sudo apt install mysql-server

Secure MySQL With the Secure Installation Script

cmd: sudo mysql_secure_installation

cmd: mysql -V

cmd: sudo service mysql status

Installing PHP

cmd : sudo apt install php-fpm php-mysql

cmd: sudo nano /etc/nginx/sites-available/wordpress.conf

server {
        listen 80;
        root /var/www/html;
        index index.php index.html index.htm index.nginx-debian.html;
        server_name 78.141.210.222;

        location / {
                try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
}

cmd: sudo ln -s /etc/nginx/sites-available/sample.com /etc/nginx/sites-enabled/

cmd: sudo unlink /etc/nginx/sites-enabled/default


cmd:sudo nginx -t

sudo systemctl reload nginx

cmd: sudo nano /var/www/html/info.php

code: <?php
phpinfo();

cmd: sudo rm info.php

Install WordPress with LEMP on Ubuntu 22.04

sudo mysql

mysql: CREATE DATABASE wordpressworld DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;

mysql: CREATE USER 'supermario'@'localhost' IDENTIFIED BY 'bowser_9Es';

mysql: GRANT ALL ON wordpressworld.* TO 'supermario'@'localhost';

mysql:EXIT;

cmd: sudo apt install php-curl php-gd php-intl php-mbstring php-soap php-xml php-xmlrpc php-zip

cmd: sudo systemctl restart php8.1-fpm


cmd: sudo nano /etc/nginx/sites-available/sample.com

And we will add a few location directives.

code:  location = /favicon.ico { log_not_found off; access_log off; }
location = /robots.txt { log_not_found off; access_log off; allow all; }
location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
    expires max;
    log_not_found off;
}
We will also adjust the try_files location. Let’s comment out the current one and add the following line underneath it.

try_files $uri $uri/ /index.php$is_args$args;

code:server {
        listen 80;
        root /var/www/html;
        index index.php index.html index.htm index.nginx-debian.html;
        server_name 3.109.209.23;

        location / {
              #  try_files $uri $uri/ =404;
              try_files $uri $uri/ /index.php$is_args$args;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }

location = /favicon.ico { log_not_found off; access_log off; }
location = /robots.txt { log_not_found off; access_log off; allow all; }
location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
    expires max;
    log_not_found off;
}
}

cmd: sudo nginx -t

cmd: systemctl reload nginx 

installtion and configuration of wordpress

cmd: cd /tmp

cmd: curl -LO https://wordpress.org/latest.tar.gz

cmd: tar xzvf latest.tar.gz

cmd: cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php

cmd: sudo cp -a /tmp/wordpress/. /var/www/html

cmd: cd /var/www/html && ls

cmd: sudo chown -R www-data:www-data /var/www/html

cmd: curl -s https://api.wordpress.org/secret-key/1.1/salt/

cmd: sudo nano /var/www/html/wp-config.php

