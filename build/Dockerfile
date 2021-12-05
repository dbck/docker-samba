FROM debian:11

LABEL maintainer "Dennis Boeckmann <dev@dbck.de>"
LABEL description "Debian based simple samba container"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get -q -y install \
    sudo \
    vim \
    samba \
    && rm -rf /var/lib/apt/lists/*

ENV SAMBA_USER SAMBA

# Samba
RUN mkdir -p /shares
RUN mv /etc/samba/smb.conf /etc/samba/smb.conf.bak
COPY root/etc/samba/* /etc/samba/

COPY root/docker-entrypoint.sh /
RUN chmod 777 /docker-entrypoint.sh

EXPOSE 445

ENTRYPOINT ["/docker-entrypoint.sh"]

#HEALTHCHECK --interval=5s --timeout=5s CMD nc -vz 127.0.0.1 445 || exit 1