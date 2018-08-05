## docker-web-proxy
A small example for Nginx HTTPS Proxy using docker-compose 
for containers based on Apache, PHP 7.0 (ionCube PHP Loader, Zend OPcache, Xdebug), Mysql and Mailhog.
PHP Container created by 
https://webdevops.io/

inspired by an article from Dominik Weber: https://dev.to/domysee/setting-up-a-reverse-proxy-with-nginx-and-docker-compose-29jg


### Setup

set your vars in ``.env``

    
### ssign the docker ip in your Hostfile usually under OSX and Linux

    vi /etc/hosts
    
write

    0.0.0.0 app.local
    
to Import a Db at Start Up. Put the SQL Dump into

    .docker/database/inital-import

Then run
    
    docker-compose up --buiild
    
You can check the PHP Settings under:
    
    https://app.local/info.php
    
### All outcoming mails are sent to MailHog ###
    
    http://app.local:8025
   