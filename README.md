# Hacking-Wordpress

# Enumeration Procedure For Wordpress Website in Manually

### Wordpress Version Check

Check Wordpress Version using given below curl command or seeing source code

    commnad:
            curl -s -X GET http://blog.inlanefreight.com | grep '<meta name="generator"'
        
 Also check WP Version - CSS and WP Version - JS version from Source Code 
 
### Plugins and Themes Enumeration

Commnad For Plugins: 
      
      curl -s -X GET http://blog.inlanefreight.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'wp-content/plugins/*' | cut -d"'" -f2
 
Command For Themmes:
      
      curl -s -X GET http://blog.inlanefreight.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'themes' | cut -d"'" -f2
      
    
#### User Enumeration
Enumerating a list of valid users is a critical phase of a WordPress security assessment. Armed with this list, we may be able to guess default credentials or perform a brute force password attack. If successful, we may be able to log in to the WordPress backend as an author or even as an administrator. This access can potentially be leveraged to modify the WordPress website or even interact with the underlying web server.

Command :
         curl http://blog.inlanefreight.com/wp-json/wp/v2/users
         
         
 
# Enumeration Procedure For Wordpress Website in Automatically Using wpscan

         

        
