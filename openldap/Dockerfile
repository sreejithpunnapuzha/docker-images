ARG FROM=quay.io/sreejithp/ubuntu:noble
FROM ${FROM}

ARG UBUNTU_RELEASE=noble

RUN echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE} main restricted universe multiverse" > /etc/apt/sources.list; \
        echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-updates main restricted universe multiverse" >> /etc/apt/sources.list; \
        echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-backports main restricted universe multiverse" >> /etc/apt/sources.list; \
        echo "deb http://security.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-security main restricted universe multiverse" >> /etc/apt/sources.list; \
        apt update && apt dist-upgrade -y; \
        apt install -y slapd ldap-utils sudo \
        && apt autoremove -y && apt clean && rm -rf /var/lib/apt/lists/*

EXPOSE 389 636
