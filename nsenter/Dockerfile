ARG FROM=quay.io/sreejithp/ubuntu:jammy
FROM ${FROM} as builder

ARG TIMEZONE=America/Chicago
ARG UTIL_LINUX_VER=2.40.3
ARG UBUNTU_RELEASE=jammy

RUN ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && echo $TIMEZONE > /etc/timezone; \
    echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE} main restricted universe multiverse" > /etc/apt/sources.list; \
    echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-updates main restricted universe multiverse" >> /etc/apt/sources.list; \
    echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-backports main restricted universe multiverse" >> /etc/apt/sources.list; \
    echo "deb http://security.ubuntu.com/ubuntu ${UBUNTU_RELEASE}-security main restricted universe multiverse" >> /etc/apt/sources.list; \
    apt-get update && apt-get dist-upgrade -y; \
    apt-get update && apt-get install -yq apt-utils git make gcc gettext autopoint bison libtool automake pkg-config flex sqlite3 asciidoctor po4a \
    && apt-get autoremove -y --purge && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /code

# download util-linux sources
ADD https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/snapshot/util-linux-${UTIL_LINUX_VER}.tar.gz .
RUN tar -xf util-linux-${UTIL_LINUX_VER}.tar.gz && mv util-linux-${UTIL_LINUX_VER} util-linux

# make static version
WORKDIR /code/util-linux
RUN ./autogen.sh && ./configure
RUN make LDFLAGS="--static" nsenter

# Final image
FROM scratch

COPY --from=builder /code/util-linux/nsenter /

ENTRYPOINT ["/nsenter"]
