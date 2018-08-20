## docker-web-proxy
Nginx HTTPS Proxy using docker-compose for containers based on Apache, PHP 7.0 (ionCube PHP Loader, Zend OPcache, Xdebug), Mysql and Mailhog. Apache Container connects to php via sockets not port as usual.

### Setup

set your vars in ``.env``

    
### assign the docker ip in your Hostfile usually under OSX and Linux

    vi /etc/hosts
    
write

    0.0.0.0 app.local
    
to Import a Db at Start Up. Put the SQL Dump into

    .docker/database/inital-import

Then run for OSX ```docker-compose -f docker-compose.mac.yml up --build``` or ```docker-compose up --build```
    
You can check the PHP Settings under:
    
    https://app.local/info.php
    
### All outcoming mails are sent to MailHog ###
    
    http://app.local:8025
   
