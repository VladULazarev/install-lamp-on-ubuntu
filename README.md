## Установка и настройка LAMP на Ubuntu 20.04

Set Up apache2:

```bash
sudo apt update
sudo apt install apache2
```

Enable Firewall management tool:

```bash
sudo apt install ufw
sudo ufw enable
```

Allow Apache Full (opens 80 и 443 ports):

```bash
sudo ufw allow 'Apache Full'
```

Open SSH:

```bash
sudo ufw allow 'OpenSSH'
```

Disable directory listing and enable AllowOverride:

```bash
sudo nano /etc/apache2/apache2.conf
```

In /etc/apache2/apache2.conf set as follows:

```bash
Options FollowSymLinks
AllowOverride All
Require all granted
```

Restart apache:

```bash
sudo systemctl restart apache2
```

Turn on mod_rewrite:

```bash
sudo a2enmod rewrite
sudo systemctl restart apache2
```

Set Up MySQL Server:

```bash
sudo apt install mysql-server
sudo systemctl restart apache2
```

Check if MySQL Server is active:

```bash
sudo systemctl status mysq
```

Set Up PHP:

```bash
sudo apt install php libapache2-mod-php php-mysql
sudo systemctl restart apache2
```

Check PHP version:

```bash
php -v
```

Set Up phpMyAdmin:

```bash
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
```

To show phpMyAdmin page in a browser:

```bash
sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
sudo a2enconf phpmyadmin.conf
sudo systemctl restart apache2
```

Check if OK:

```bash
http://your_domain_or_IP/phpmyadmin
```

Configuring Password Access for the MySQL Root Account:

```bash
sudo mysql
SELECT user,authentication_string,plugin,host FROM mysql.user;
ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'your_password';

quit
```

Check if OK:

```bash
http://your_domain_or_IP/
```

