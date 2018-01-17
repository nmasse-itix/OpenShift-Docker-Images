FROM registry.access.redhat.com/rhel7:latest

RUN curl -L -o /usr/local/bin/minio https://dl.minio.io/server/minio/release/linux-amd64/minio \
 && chmod 755 /usr/local/bin/minio \
 && mkdir /var/lib/minio /etc/minio \
 && chmod -R ugo+rw,+X /var/lib/minio /etc/minio

VOLUME /var/lib/minio
WORKDIR /var/lib/minio

EXPOSE 9000
ENTRYPOINT [ "/usr/local/bin/minio" ]
CMD [ "server", "--config-dir", "/etc/minio", "/var/lib/minio" ]
