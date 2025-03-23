# Apache, MySQL and PHP
Installing AMP on Fedora

Resources - Fedora documentation for:
- [Apache](https://docs.fedoraproject.org/en-US/quick-docs/getting-started-with-apache-http-server/)
- [MySQL/MariaDB](https://docs.fedoraproject.org/en-US/quick-docs/installing-mysql-mariadb/)
- [PHP](https://developer.fedoraproject.org/tech/languages/php/php-installation.html)


## Apache server
Install
```bash
$ sudo dnf install httpd
```
Check status
```bash
$ systemctl status httpd.service
```

Enable the service
```bash
$ sudo systemctl enable httpd.service
```
Start the service
```bash
$ sudo systemctl start httpd.service
```
Re-check the status

## MySQL or MariaDB
Install
```bash
$ sudo dnf install mariadb-server
```
Check status
```bash
$ systemctl status mariadb
```
Enable and start the service
```bash
$ sudo systemctl enable mariadb
$ sudo systemctl start mariadb
```
Recheck the status

### Configure MySQl
```bash
$ sudo mysql_secure_installation
# Create mysql password
```
Follow on-screen instructions

### Test MySQL
Start MySQL
```bash
$ sudo mysql -u root -p
# Enter the mysql password
```
List out the databases
```sql
> SHOW DATABASES;
```
Quit by typing `\q`

## PHP
Install PHP and it's extensions
```bash
$ sudo dnf install php php-cli phpunit composer php-mysqlnd
```

Check the permissions of `/var/www/html` directory
```bash
$ ll /var/www
```

Change ownership and check the updated ownership
```bash
$ sudo chown -R anwesh:anwesh /var/www/html
$ ll /var/www
```

Create `index.html` file in the above directory with some text
```bash
$ echo "Test" > /var/www/html/index.html
```
Open localhost with a browser
```bash
$ firefox localhost
```

Rename the `index.html` as `index.php`
```bash
$ mv /var/www/html/index.html /var/www/html/index.php
```

Restart apache
```bash
$ sudo systemctl restart httpd.service
```

Edit the `index.php` file (optional)
```bash
$ echo "This line was added after installing PHP" > /var/www/html/index.php
```

Reopen localhost

This time the above PHP file gets rendered.