/*
Title: Apache subdomains 
Description: Apache subdomains setup 
Date: 2013/11/11
Author: Philipp Schmitt
Tags: apache,virtualhost
*/

Everybody loves subdomains, but how do you set them up ?

## Define subdomains (ArchLinux)

In order to add a subdomain, you gotta start off with editing your DNS settings by adding an A Record pointing to your domain, like:
    
    Hostname     Type  Value
    sub          A     78.46.88.98

Then you need to add `Include conf/extra/httpd-vhosts.conf` to your apache config (`/etc/httpd/conf/httpd.conf`) and edit this file accordingly:

    <VirtualHost *:80>
        DocumentRoot "/srv/http/schmitt.co"
        ServerName   schmitt.co
    </VirtualHost>

    <VirtualHost *:80>
        DocumentRoot "/srv/http/sub.schmitt.co"
        ServerName   sub.schmitt.co 
    </VirtualHost> 

This defines a subdomain whose root is located at `/srv/http/sub.schmitt.co`.

In order to make our server aware of this subdomain one last step is necessary, namely an entry in `/etc/hosts`:

    #
    # /etc/hosts: static lookup table for host names
    #

    #<ip-address>   <hostname.domain.org>   <hostname>
    127.0.0.1       localhost.localdomain   localhost
    ::1             localhost.localdomain   localhost
    127.0.0.1       schmitt.co    
    127.0.0.1       sub.schmitt.co

## Per subdomain config

Now that we have defined our subdomain we may want to edit the corresponding apache options. This can be done easily by adding a `Directory` section to `httpd-vhosts.conf`. Let's say we want to enable caching on our subdomain:

    <VirtualHost *:80>
        DocumentRoot "/srv/http/sub.schmitt.co"
        ServerName  sub.schmitt.co 
        <Directory /srv/http/sub.schmitt.co>
            ExpiresActive On
            ExpiresDefault "access plus 1 hour"
        </Directory>
    </VirtualHost>

