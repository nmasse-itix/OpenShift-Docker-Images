FROM registry.access.redhat.com/rhel7:latest

ADD rsyslog.conf /etc/rsyslog.conf
RUN yum update -y \
 && yum -y install rsyslog \
 && yum clean all \
 && rm -rf /var/cache/yum \
 && chmod -R ugo+rw,+X /etc/rsyslog.conf /var/log/ /var/run/

VOLUME /var/log/
WORKDIR /var/log/

EXPOSE 1601
ENTRYPOINT [ "/usr/sbin/rsyslogd" ]
CMD [ "-4", "-n", "-f", "/etc/rsyslog.conf", "-i", "/var/run/rsyslog.pid" ]

