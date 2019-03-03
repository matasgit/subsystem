<h1>Cheatsheet on how to set up Windows subsystem for Linux (WSL) for the local development</h1>
<p>Linux, Node.js, npm, Git, Apache, PHP, PostgreSQL</p>

<h2>Install subsystem</h2>
<ul>
        <li>press win key</li>
        <li>type Turn Windows Features on or of</li>
        <li>tick Windows Subsystem for Linux</li>
        <li>go to MS store and install your flavor of linux</li>
</ul>

<h2>Install node and npm</h2>
<ul>
        <li>sudo apt install curl</li> 
        <li>url -sL https://deb.nodesource.com/setup_11.x | sudo bash -</li>
        <li>sudo apt install nodejs</li>
</ul>
<p>replace setup_11.x with current version</li>

<h2>install git</h2>
<ul>
        <li>sudo apt install git</li>
</ul>

<h2>install and set up apache, php, postgresql</h2>
<ul>
        <li>sudo apt install apache2</li>
        <li>sudo apt install postgresql postgresql-contrib</li>
        <li>sudo apt install php</li>
</ul>

<h3>restart apache and postgres</h3>
<ul>
        <li>sudo service apache2 restart</li>
        <li>sudo service postgresql restart</li>
</ul>

<h3>set postgres password (to connect from pgAdmin etc)</h3>
<ul>
        <li>sudo su postgres (enter your pass)</li>
        <li>psql</li>
        <li>\password</li>
        <li>\q</li>
</ul>

<h3>create a symlink between windows projects folder and folder on linux subsystem e.g.</h3>
<ul>
        <li>sudo ln -s /mnt/c/projects /var/www/devroot</li>
</ul>

<h3>setup vhost e.g.</h3>
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

<h3>edit hosts file on Windows</h3>
<ul>
        <li>press win key</li>
        <li>type in Notepad</li>
        <li>right click and open as Administrator</li>
        <li>with the Notepad open the C:\Windows\System32\Drivers\etc\hosts (make sure all files are selected in the file type dropdown)</li>
        <li>add a new line 127.0.0.1 www.test.local</li>
</ul>

<h3>do not bell on tab-completion</h3>
<ul>
        <li>sudo nano /etc/inputrc</li>
        <li>uncomment set bell-style none</li>
</ul>
