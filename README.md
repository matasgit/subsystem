--install subsystem
1) press win key
2) type Turn Windows Features on or of
3) tick Windows Subsystem for Linux
4) go to MS store and install your flavor of linux

--Install node and npm
1) sudo apt install curl 
2) curl -sL https://deb.nodesource.com/setup_11.x | sudo bash -
3) sudo apt install nodejs
(replace setup_11.x with current version)


--Install git
1) sudo apt install git


--Install stack
1) sudo apt-get install apache2
2) sudo apt install postgresql postgresql-contrib
3) sudo apt-get install php

-Restart apache and postgres
sudo service apache2 restart
sudo service postgresql restart

-set postgres password (to connect from pgAdmin etc)
sudo su postgres (enter your pass)
psql
\password
\q

-Create a symlink between windows projects folder and folder on linux subsystem e.g.
sudo ln -s /mnt/c/projects /var/www/devroot

-Setup vhost on linux subsystem e.g.
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

-Edit hosts file on windows
1) Press windows key
2) Type in Notepad
3) Right click and open as Administrator
4) With the Notepad open the C:\Windows\System32\Drivers\etc\hosts (make sure all files are selected)
5) Add a new line 127.0.0.1 www.test.local


-------------------
disable bash sound
To disable the beep of the bash you need to uncomment (add if not already there):
set bell-style none in your /etc/inputrc file. 
Note: Since it is a read-only file you will need to be a sudoer.





