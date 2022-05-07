# 🔥Wordpress Structure 🔥

WordPress can be installed on a Windows, Linux, or Mac OSX host. For this module, we will focus on a default WordPress installation on an Ubuntu Linux web server. WordPress requires a fully installed and configured LAMP stack (Linux operating system, Apache HTTP Server, MySQL database, and the PHP programming language) before installation on a Linux host. After installation, all WordPress supporting files and directories will be accessible in the webroot located at /var/www/html.

Below is the directory structure of a default WordPress install, showing the key files and subdirectories necessary for the website to function properly.


     tree -L 1 /var/www/html
.
     ├── index.php
     ├── license.txt
     ├── readme.html
     ├── wp-activate.php
     ├── wp-admin
     ├── wp-blog-header.php
     ├── wp-comments-post.php
     ├── wp-config.php
     ├── wp-config-sample.php
     ├── wp-content
     ├── wp-cron.php
     ├── wp-includes
     ├── wp-links-opml.php
     ├── wp-load.php
     ├── wp-login.php
     ├── wp-mail.php
     ├── wp-settings.php
     ├── wp-signup.php
     ├── wp-trackback.php
     └── xmlrpc.php
