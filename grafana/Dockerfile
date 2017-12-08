FROM registry.access.redhat.com/rhel7:latest

ADD grafana.repo /etc/yum.repos.d/grafana.repo
RUN yum update -y \
 && yum -y install grafana fontconfig freetype urw-fonts\
 && yum clean all \
 && rm -rf /var/cache/yum \
 && chmod -R ugo+rw,+X /var/lib/grafana/ /var/run/ /var/log/grafana /etc/grafana/

VOLUME /var/lib/grafana/ /var/run/grafana /var/log/grafana
WORKDIR /usr/share/grafana/

EXPOSE 3000
ENTRYPOINT [ "/usr/sbin/grafana-server" ]
CMD [ "--pidfile=/var/run/grafana.pid", "--config=/etc/grafana/grafana.ini", "cfg:default.paths.data=/var/lib/grafana/", "cfg:default.paths.logs=/var/log/grafana", "cfg:default.paths.plugins=/var/lib/grafana/plugins" ]
