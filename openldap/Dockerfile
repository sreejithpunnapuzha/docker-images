ARG FROM=quay.io/sreejithp/ubuntu:noble
FROM ${FROM}

ARG UBUNTU_RELEASE=noble

RUN echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE} main restricted universe multiverse" > /etc/apt/sources.list; \
        echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-updates main restricted universe multiverse" >> /etc/apt/sources.list; \
        echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-backports main restricted universe multiverse" >> /etc/apt/sources.list; \
        echo "deb http://security.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-security main restricted universe multiverse" >> /etc/apt/sources.list; \
        apt update && apt dist-upgrade -y; \
        LC_ALL=C DEBIAN_FRONTEND=noninteractive apt install -y slapd ldap-utils sudo \
        && apt autoremove -y && apt clean && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/* && rm -rf /var/tmp/*

# Default configuration: can be overridden at the docker command line
ENV LDAP_ROOTPASS toor
ENV LDAP_ORGANISATION Aastha Inc.
ENV LDAP_DOMAIN aastha.inc

EXPOSE 389 636

RUN mkdir /etc/service/slapd
ADD slapd.sh /etc/service/slapd/run

# To store config outside the container, mount /etc/ldap/slapd.d as a data volume.
# To store data outside the container, mount /var/lib/ldap as a data volume.
VOLUME /etc/ldap/slapd.d /var/lib/ldap
