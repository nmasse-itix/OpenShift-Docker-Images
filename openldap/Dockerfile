FROM centos:7

RUN yum update -y && yum -y install openldap-servers openldap-clients && yum clean all && chgrp -R root /var/lib/ldap && chmod -R g+rw,o= /var/lib/ldap

VOLUME /var/lib/ldap
WORKDIR /var/lib/ldap

EXPOSE 389 636
ENTRYPOINT [ "/usr/sbin/slapd" ]
CMD [ "-4" ]

