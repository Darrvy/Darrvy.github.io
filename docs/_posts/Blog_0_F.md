---
layout: post
title:  "Blog 0"
date:   2020-09-01 20:02:38 -0700
categories: jekyll update
---
<h1>Turning Raspberry Pi into LAMP (Linux Apache MySQL PHP) Server</h1>
<p>
So I’ve had a raspberry pi sitting around for a while and I decided to turn it into a LAMP server. I plan to do this so I can host and practice some web development things and to put the pi to some use.
<br><br>
The first thing I wanted to do was to be able to access my raspberry pi’s terminal from my computer. To do this I connected my raspberry pi to my tv, got onto the settings for my pi, and enabled SSH. Once I had this all done, all I had to do left was to get IP for my pi which I used the command below to output my IP.
</p>

<code>ifconfig -a</code>

<p>
Once I had the IP I didn’t need to be connected to a tv or need any accessories to access the pi. To access the pi from my computer I needed to run the command below and put in the password for my pi.
</p>

<code>ssh pi@my_pi__IP</code>

At this point, I was able to access the pi’s terminal using Powershell. From here I just had to update my pi so I used the commands below.

<code>sudo apt update</code>

and

<code>sudo apt full-upgrade</code>

<h2>Apache</h2>

Once I had my pi update it was time to install Apache.

<code>sudo apt install apache2 -y</code> 

Once everything has finished installing all I have to do now is use the IP of my pi on a web browser and it will show me the default web page indicating that apache is working and information to where the config files are at. 

From here I had to change directories to where the index.html file is

<code>cd /var/www/html</code>

Then by using the command <code>ls</code> I was able to see the index.html file. 

From here I got the webserver going and can use commands to check the status, stop the server, start the server and restart it.

<code>service apache2 status</code>

<code>sudo service apache2 start</code>

<code>sudo service apache2 restart</code>

<code>sudo service apache2 stop</code>

<h2>PHP</h2> 

Now it is time to install PHP onto my raspberry pi using the command 

<code>sudo apt install php -y</code>

Once I installed php I changed directories back to <code>/var/www/html</code> and removed the index_html file

<code>sudo rm index.html</code> 

And then created a php file with a small script to make sure that it was working properly.

<code>sudo vi index.html</code>

Once I created the script I restarted my apache server and the php script worked. 

<h2>MySQL</h2>

Now I installed MySQLServer by running the command

<code>sudo apt install mariadb-server php-mysql -y</code>

And once it was installed I ran the command 

<code>sudo mysql_secure_installation</code>

This secures the MYSQL installation

From here I was prompted with my password for root and then prompted with other questions with setting up the Mariadb and once I was done I was prompted with the message “Thanks for using MariaDB!”.

<h2>PHPMyAdmin</h2> 

Now it is time to install the PHPMyAdmin on the pi.

<code>sudo apt install phpmyadmin -y</code> 

During the installation i was prompted with a prompt to configure the PHPMyAdmin.

The first prompt I selected apache2 

The Second prompt “Configure database for phpmyadmin with dbconfig-common? I selected Yes

Then i was prompted to enter my password

After that I used the command 

<code>sudo phpenmod mysqli</code> 

To enable the PHP MYSQL extension 

I then restarted my apache server

<code>sudo service apache2 restart</code>

From here I wanted to make sure that the PHPMyAdmin was working so I put my IP followed by PHPMyAdmin in my browser to make sure it worked

<code>my_IP/phpmyadmin</code> 

It was giving me an error at first so I had to move the PHPMyAdmin folder onto my <code>/var/www/html</code> folder. I used the command     
<code>sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin</code>

Now I refreshed the web page and the PHPMyAdmin page was working properly. Also by using ls i was able to verify that the file was moved over.

Now that I have the PHPMyAdmin I came to a new issue and that was that I was not able to log in. To fix this issue I had to create a username, password, and grant the user privileges.

To do this I had to run the command 

<code>sudo mysql</code>

<code>>CREATE USER ‘your_username’@’localhost’ IDENTIFIED BY ‘your_password’;</code>
<br>
<code>>GRANT ALL PRIVILEGES  ON *.* TO ‘your_username’@’localhost;</code>
<br>
<code>>FLUSH PRIVILEGES;</code>
<br>
<code>>exit</code>

Now that all this was done I had my LAMP server done.

<strong>Note:</strong> Will do this over to include images.
