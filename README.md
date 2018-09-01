## docker-web-proxy
Nginx HTTPS Proxy using docker-compose for containers based on Apache, PHP 7.0 (ionCube PHP Loader, Zend OPcache, Xdebug), Mysql and Mailhog. Apache Container connects to php via sockets not port as usual.

### Setup

set your vars in ``.env``
    
to Import a Db at Start Up. Put the SQL Dump into

    .docker/database/inital-import

You can check the PHP Settings under:
    https://localhost/info.php
    
### All outcoming mails are sent to MailHog
    http://localhost:8025
   
