FROM centos:7

RUN yum update -y \
 && yum -y install openldap-servers openldap-clients \
 && yum clean all \
 && rm -rf /var/cache/yum \
 && cp /usr/share/openldap-servers/DB_CONFIG.example /var/lib/ldap/DB_CONFIG \
 && chgrp -R root /var/lib/ldap \
 && chmod -R g+rw,o= /var/lib/ldap

VOLUME /var/lib/ldap
WORKDIR /var/lib/ldap

EXPOSE 1389
ENTRYPOINT [ "/usr/sbin/slapd" ]
CMD [ "-d", "256", "-h", "ldap://0.0.0.0:1389/" ]
