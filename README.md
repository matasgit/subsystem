# Cheatsheet on how to setup Windows subsystem for Linux (WSL2) for the local development

Linux, Node.js, npm, Git, Apache, PHP, PostgreSQL


## Install subsystem

* press win key
* type Turn Windows Features on or of
* tick Windows Subsystem for Linux
* go to MS store search and install your flavor of linux
* go to MS store search and install Windows Terminal


## Install and setup Node.js and npm

* sudo apt install curl 
* curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
* sudo apt install nodejs

replace 14 with current version</li>


## (ignore if the step above worked well) Update Node.js and npm to the latest version

* sudo npm cache clean -f
* sudo npm install -g n
* sudo n latest

sudo n stable for the stabel version


## Install and setup Git

* sudo apt install git
* git config --global user.email "you@example.com"
* git config --global user.name "Your Name"


## Install and set up Apache, PHP

* sudo apt install apache2
* sudo apt install php


## Install PostgreSQL

### latest for Debian

* sudo apt install wget ca-certificates
* sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
* wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

### latest for Ubuntu

* sudo apt install wget ca-certificates
* wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
* sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ \`lsb_release -cs\`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

### run this for either

* sudo apt-get update
* sudo apt install postgresql postgresql-contrib


### Restart Apache and PostgreSQL (you might be getting some warnings/errors for apache but I think it's safe to ignore them)

* sudo service apache2 restart
* sudo service postgresql restart


### Set postgres password (to connect from pgAdmin etc)

* sudo su postgres (enter your pass)
* psql
* \password
* \q


### Create a symlink between Windows projects folder and folder on Linux subsystem e.g.

* sudo ln -s /mnt/c/projects /var/www/devroot


### Setup vhost e.g.
```
<VirtualHost *:80>
        ServerName www.test.local
        ServerAdmin mac@localhost
        DocumentRoot /var/www/devroot/test

        <Directory /var/www/>
          Options Indexes FollowSymLinks
          AllowOverride All
          Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/testerror.log
        CustomLog ${APACHE_LOG_DIR}/testaccess.log combined
</VirtualHost>
```


### Edit hosts file on Windows

* press win key
* type in Notepad
* right click and open as Administrator
* with the Notepad open the C:\Windows\System32\Drivers\etc\hosts (make sure all files are selected in the file type dropdown)
* add a new line 127.0.0.1 www.test.local


## Disable terminal's bell sound on tab-completion (optional if using Windows Terminal)

* sudo nano /etc/inputrc
* uncomment set bell-style none


## Uning default terminal colours in tmux (optional if using Windows Terminal)

* nano ~/.tmux.conf
* paste in
```
set -g default-terminal "xterm-256color"
set-option -ga terminal-overrides ",xterm-256color:Tc"
```


## Posh terminal

Follow this tutorial
https://www.hanselman.com/blog/HowToMakeAPrettyPromptInWindowsTerminalWithPowerlineNerdFontsCascadiaCodeWSLAndOhmyposh.aspx
