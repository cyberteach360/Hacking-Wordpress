# π₯Wordpress Structure π₯

WordPress can be installed on a Windows, Linux, or Mac OSX host. For this module, we will focus on a default WordPress installation on an Ubuntu Linux web server. WordPress requires a fully installed and configured LAMP stack (Linux operating system, Apache HTTP Server, MySQL database, and the PHP programming language) before installation on a Linux host. After installation, all WordPress supporting files and directories will be accessible in the webroot located at /var/www/html.

Below is the directory structure of a default WordPress install, showing the key files and subdirectories necessary for the website to function properly.


     tree -L 1 /var/www/html

     βββ index.php
     βββ license.txt
     βββ readme.html
     βββ wp-activate.php
     βββ wp-admin
     βββ wp-blog-header.php
     βββ wp-comments-post.php
     βββ wp-config.php
     βββ wp-config-sample.php
     βββ wp-content
     βββ wp-cron.php
     βββ wp-includes
     βββ wp-links-opml.php
     βββ wp-load.php
     βββ wp-login.php
     βββ wp-mail.php
     βββ wp-settings.php
     βββ wp-signup.php
     βββ wp-trackback.php
     βββ xmlrpc.php
## Key WordPress Files

The root directory of WordPress contains files that are needed to configure WordPress to function correctly.

    index.php is the homepage of WordPress.

    license.txt contains useful information such as the version WordPress installed.

    wp-activate.php is used for the email activation process when setting up a new WordPress site.

    wp-admin folder contains the login page for administrator access and the backend dashboard. Once a user has logged in, they can make changes to the site based on their assigned permissions. The login page can be located at one of the following paths:
    /wp-admin/login.php
    /wp-admin/wp-login.php
    /login.php
    /wp-login.php

This file can also be renamed to make it more challenging to find the login page.

    xmlrpc.php is a file representing a feature of WordPress that enables data to be transmitted with HTTP acting as the transport mechanism and XML as the encoding mechanism. This type of communication has been replaced by the WordPress REST API.
