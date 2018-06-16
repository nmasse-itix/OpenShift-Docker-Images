FROM centos:7

RUN yum update -y \
 && yum -y install rtorrent expect \
 && yum clean all \
 && rm -rf /var/cache/yum \
 && mkdir /torrent /etc/rtorrent

# Where leeched / seeded files are stored
VOLUME /torrent/download

# Where to drop .torrent files (will be picked up automatically by rtorrent)
VOLUME /torrent/incoming

# Where rtorrent stores its internal files
VOLUME /torrent/session

WORKDIR /torrent

# Standard Bittorrent Port
EXPOSE 6890/tcp
EXPOSE 6890/udp

# DHT Port
EXPOSE 6881/udp

# Standard configuration
ADD rtorrent.rc /etc/rtorrent.rc
ADD custom.rc /etc/rtorrent/custom.rc

# The unbuffer command is used as entrypoint to fake a tty.
# It is required since the daemon mode will only be available 
# with rtorrent 0.9.7.
ENTRYPOINT [ "/bin/unbuffer" ]
CMD [ "/bin/rtorrent", "-n", "-o", "import=/etc/rtorrent.rc", "-o", "import=/etc/rtorrent/custom.rc" ]

