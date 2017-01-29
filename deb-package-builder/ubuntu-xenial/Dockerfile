FROM ubuntu:xenial

RUN echo 'APT::Install-Recommends "0";' >>/etc/apt/apt.conf.d/99-recommends && \
    echo 'APT::Install-Suggests "0";' >>/etc/apt/apt.conf.d/99-suggests && \
    echo "alias d='ls -al --color'" >>/root/.bashrc && \
    apt -y update && \
    apt -y dist-upgrade && \
    apt -y install gettext \
                   automake \
                   libtool \
                   pkg-config \
                   wget \
                   dh-make \
                   devscripts \
                   fakeroot

ENV VERSION 7.08
ENV DEBFULLNAME "Guillaume LECERF"
ENV DEBEMAIL "glecerf@gmail.com"

RUN apt -y install libssl-dev \
                   libxml2-dev \
                   liblz4-dev \
                   libstoken-dev \
                   libp11-dev \
                   libp11-kit-dev \
                   liboath-dev

RUN mkdir -p /packaging && \
    cd /packaging && \
    wget -q ftp://ftp.infradead.org/pub/openconnect/openconnect-${VERSION}.tar.gz && \
    cp openconnect-${VERSION}.tar.gz openconnect-${VERSION}.orig.tar.gz && \
    tar xzf openconnect-${VERSION}.tar.gz

RUN cd /packaging/openconnect-${VERSION} && \
    dh_make -s -y -f ../openconnect-${VERSION}.orig.tar.gz && \
    echo 'override_dh_auto_configure:' >>debian/rules && \
    echo '\tdh_auto_configure -- --with-vpnc-script=/etc/vpnc/vpnc-script --without-openssl-version-check' >>debian/rules && \
    debuild -us -uc -d
