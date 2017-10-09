# ==================|Install MySQL server with Workbench(Admin tool)|==================
Create date: 2017-10-09
### Install Ubuntu server on a Virtual Machine
  You can use VMWare or Virtualbox as your tool.
  1. Download `ubuntu-16.04.3-server-amd64` from Ubuntu website.
  2. Install it to your VM machine.
  3. Run command `sudo apt-get update -y && sudo apt-get upgrade -y`
      - If you have issue with `dpkg`, please use following method(works for 16.04)
        * `cd /var/lib/dpkg/updates directory`
        * `sudo rm *`
        * `sudo apt-get update`
  4. Now your machine is ready for WebServer(Apache2), Database(MySQL) and Operating script(PHP) 
 
        
### Install Apache2 web server
  1. In Ubuntu server, type `sudo apt-get install apache2` to install Apache2 web server.
  2. After the installation is complete, you may want to setup the DOMAIN name or IP in `/etc/apache2/apache2.conf` file. `ServerName server_domain_or_IP`
  3. Restart the service once, `service apache2 restart`
  4. Test our web service configuration `sudo apache2ctl configtest`
  5. Make sure that your firewall allows HTTP and HTTPS traffic using `sudo ufw app list`, we should have **Apache Full** in the list to ensure HTTP and HTTPS are allow by our firewall. to see the detail `sudo ufw app info "Apache Full"`
  6. Test access the website `http://your_server_IP_address`

### Install PHP7
  1. `apt-get -y install php7.0 libapache2-mod-php7.0`
  2. Everytime you create `.php` file make sure it has "READ" permission unless you can't open it via browser

### Install FTP for easier file transfer to server
  1. `sudo apt install vsftpd`
  2. Change setting of `/etc/vsftpd.conf` to allow uploading, Uncomment `write_enable=YES`
  3. Restart vsftpd service `service vsftpd restart`
  4. Connect to this host via any FTP tool(e.g. WinSCP, FileZilla)
  
### Install MySQL and connect to MySQL database
  1. `sudo apt-get install mysql-server`
  2. `mysql_secure_installation` to harden your database.
  3. Login to MySQL server `mysql -u root -p`
  4. If you want to change password then `ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';`
  5. Create new user to work with database since `root` is not recommended to use for Select,Insert,Update,Delete.
      - Create use to login remotely `CREATE USER 'myuser'@'%' IDENTIFIED BY 'mypassword';`
      - Allow the user to work with target database or all database `GRANT ALL ON *.* TO 'myuser'@'%';`
      - Refresh privileges `FLUSH PRIVILEGES;`
  6. Allow user to login remotely, since we not allow `root` to login remotely. edit file `/etc/mysql/mysql.conf.d/mysqld.cnf` at `bind-address = 127.0.0.1` to `bind-address = 0.0.0.0`, or just comment this line out.
  7. Restart mysql service, `service mysql restart`
  8. Install MysqlWorkbench on client machine and try connect to the MySQL server.
    
