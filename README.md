<h1>install subsystem</h1>

1) press win key
2) type Turn Windows Features on or of
3) tick Windows Subsystem for Linux
4) go to MS store and install your flavor of linux


+----------------------+
| install node and npm |
+----------------------+

1) sudo apt install curl 
2) curl -sL https://deb.nodesource.com/setup_11.x | sudo bash -
3) sudo apt install nodejs

(replace setup_11.x with current version)


+-------------+
| install git |
+-------------+

1) sudo apt install git


+-----------------------------------+
| install apache / php / postgresql |
+-----------------------------------+

1) sudo apt install apache2
2) sudo apt install postgresql postgresql-contrib
3) sudo apt install php

--restart apache and postgres
1) sudo service apache2 restart
2) sudo service postgresql restart

--set postgres password (to connect from pgAdmin etc)
1) sudo su postgres (enter your pass)
2) psql
3) \password
4) \q

--create a symlink between windows projects folder and folder on linux subsystem e.g.
1) sudo ln -s /mnt/c/projects /var/www/devroot

--setup vhost on linux subsystem e.g.
<VirtualHost *:80>
        ServerName www.test.local
        ServerAdmin mac@localhost
        DocumentRoot /var/www/devroot/projects/test

        <Directory /var/www/>
          Options Indexes FollowSymLinks
          AllowOverride All
          Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/testerror.log
        CustomLog ${APACHE_LOG_DIR}/testaccess.log combined
</VirtualHost>

--edit hosts file on windows
1) press win key
2) type in Notepad
3) right click and open as Administrator
4) with the Notepad open the C:\Windows\System32\Drivers\etc\hosts (make sure all files are selected in the file type dropdown)
5) add a new line 127.0.0.1 www.test.local


+-------------------------------+
| do not bell on tab-completion |
+-------------------------------+

1) sudo nano /etc/inputrc
2) uncomment set bell-style none
