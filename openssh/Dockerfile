ARG FROM=quay.io/sreejithp/ubuntu:jammy
FROM ${FROM}

ARG UBUNTU_RELEASE=jammy

RUN echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE} main restricted universe multiverse" > /etc/apt/sources.list; \
        echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-updates main restricted universe multiverse" >> /etc/apt/sources.list; \
        echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-backports main restricted universe multiverse" >> /etc/apt/sources.list; \
        echo "deb http://security.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-security main restricted universe multiverse" >> /etc/apt/sources.list; \
        echo "deb http://archive.canonical.com/ubuntu ${UBUNTU_RELEASE} partner" >> /etc/apt/sources.list; \
        apt update && apt dist-upgrade -y; \
        apt install -y openssh-server openssh-client sudo \
        && apt autoremove -y && apt clean && rm -rf /var/lib/apt/lists/*

RUN mkdir /var/run/sshd; \
    mkdir /root/.ssh; \
    ssh-keygen -A; \
    chmod 0700 /root/.ssh; \
    echo 'root:myp@ssw0rd' | chpasswd; \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config; \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

EXPOSE 22

CMD ["/usr/sbin/sshd","-D", "-e"]
