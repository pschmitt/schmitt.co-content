/*
Title: Apache subdomains 
Description: Apache subdomains setup 
Date: 2013/11/11
Author: Philipp Schmitt
Tags: apache,virtualhost
*/

# Define subdomains (ArchLinux)

In order to add a subdomain, you gotta start off with editing your DNS settings by adding an A Record pointing to your domain, like:
    
    Hostname     Type  Value
    sub          A     78.46.88.98

Then you need to add `Include conf/extra/httpd-vhosts.conf` to your apache config (`/etc/httpd/conf/httpd.conf`) and edit this file accordingly:

    <VirtualHost *:80>
        DocumentRoot "/srv/http/schmitt.co"
        ServerName schmitt.co
    </VirtualHost>

    <VirtualHost *:80>
        DocumentRoot "/srv/http/sub.schmitt.co"
        ServerName  sub.schmitt.co 
    </VirtualHost> 

This defines a subdomain whose server root is located at `/srv/http/subdomain`.

In order to make our server aware of this subdomain one last step is necessary, namely an entry in `/etc/hosts`:

    #
    # /etc/hosts: static lookup table for host names
    #

    #<ip-address>   <hostname.domain.org>   <hostname>
    127.0.0.1       localhost.localdomain   localhost
    ::1             localhost.localdomain   localhost
    127.0.0.1       schmitt.co    
    127.0.0.1       sub.schmitt.co
