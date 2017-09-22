FROM centos:7

ADD DB_CONFIG /var/lib/ldap/DB_CONFIG
RUN yum update -y \
 && yum -y install openldap-servers openldap-clients \
 && yum clean all \
 && rm -rf /var/cache/yum \
 && mkdir -p /var/lib/ldap/{logs,data,tmp} \
 && chmod -R ugo+rw,+X /var/lib/ldap /var/run /etc/openldap 

VOLUME /var/lib/ldap/logs /var/lib/ldap/data /var/lib/ldap/tmp
WORKDIR /var/lib/ldap

EXPOSE 1389
ENTRYPOINT [ "/usr/sbin/slapd" ]
CMD [ "-d", "256", "-h", "ldap://0.0.0.0:1389/ ldapi:///" ]
