## docker-web-proxy
Nginx HTTPS Proxy using docker-compose for containers based on Apache, PHP 7.0 (ionCube PHP Loader, Zend OPcache, Xdebug), Mysql and Mailhog. Apache Container connects to php via sockets not port as usual.

### Setup

set your vars in ``.env``
    
to Import a Db at Start Up. Put the SQL Dump into

    .docker/database/inital-import

# start docker
    docker-compose build
    docker-compose up -d
    
### All outgoing mails are sent to MailHog
    http://app.doc:8025
    
change ``sendmail_path``in ``php-ini-overrides.ini`` to change this behaviour
   
