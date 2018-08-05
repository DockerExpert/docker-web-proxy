FROM mysql:5.7

RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get autoremove -y

COPY conf/dev.cnf /etc/mysql/conf.d/dev.cnf
COPY conf/remote-access.cnf /etc/mysql/conf.d/remote-access.cnf
COPY conf/performance-schema.cnf /etc/mysql/conf.d/performance-schema.cnf

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
