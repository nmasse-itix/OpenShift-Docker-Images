FROM centos:7

ADD DB_CONFIG /var/lib/ldap/DB_CONFIG
RUN yum update -y \
 && yum -y install openldap-servers openldap-clients \
 && yum clean all \
 && rm -rf /var/cache/yum \
 && mkdir -p /var/lib/ldap/logs /var/lib/ldap/data \
 && chmod -R ugo+rw,+X /var/lib/ldap /var/run/openldap \
 && chmod -R ugo+r,+X /etc/openldap

VOLUME /var/lib/ldap/logs /var/lib/ldap/data
WORKDIR /var/lib/ldap

EXPOSE 1389
ENTRYPOINT [ "/usr/sbin/slapd" ]
CMD [ "-d", "256", "-h", "ldap://0.0.0.0:1389/" ]
