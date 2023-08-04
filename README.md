# wordpress-projects-

#Install Nginx, MySQL/MariaDB, and PHP:
sudo apt update
sudo apt install nginx mysql-server php-fpm php-mysql
#Run the MySQL secure installation script:
sudo mysql_secure_installation
#Create a new MySQL database and user for WordPress.
#Download and configure WordPress:
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzvf latest.tar.gz
sudo mv wordpress/* .
sudo chown -R www-data:www-data /var/www/html
#Create an Nginx server block configuration for your WordPress site:
sudo nano /etc/nginx/sites-available/yourdomain.com
#Sample Nginx configuration:
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;
    root /var/www/html;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; # Check your PHP version
    }

    location ~ /\.ht {
        deny all;
    }
}
#Enable the configuration:
sudo ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx

#Install Certbot (Let's Encrypt client):
sudo apt install certbot python3-certbot-nginx
#Obtain an SSL certificate:
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
#mplement caching, gzip compression, and other optimizations in the Nginx configuration. Here are a #few settings:
gzip on;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
fastcgi_cache_path /var/cache/nginx levels=1:2 keys_zone=WORDPRESS:100m inactive=60m;




