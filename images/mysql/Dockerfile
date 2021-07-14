FROM mysql:5

LABEL ru.msav.image.authors="Andrey Mishchenko <info@msav.ru>"

ARG TIMEZONE="Europe/Moscow"

RUN apt-get update && \
    apt-get -y --no-install-recommends install \
    locales \
    tzdata \
    wget \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo ${TIMEZONE} > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata

ADD ./dev.cnf /etc/mysql/conf.d/zzz-dev.cnf
#ADD mysqltuner.pl /root/mysqltuner.pl

RUN wget http://mysqltuner.pl/ -O /root/mysqltuner.pl --no-check-certificate

RUN chown root:root /root/mysqltuner.pl \
    && chmod 775 /root/mysqltuner.pl

CMD ["mysqld"]

EXPOSE 3306
