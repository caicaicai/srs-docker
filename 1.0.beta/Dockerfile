FROM debian:wheezy

RUN \
    apt-get update && \
    apt-get install -y --force-yes --no-install-recommends libpcre3 zlib1g && \
    apt-get install -y --force-yes --no-install-recommends automake autoconf libtool build-essential wget ca-certificates unzip libpcre3-dev zlib1g-dev && \
    mkdir -p /data/install && \
    cd /data/install && \
    wget https://github.com/ossrs/srs/archive/v2.0-r2.tar.gz && \
    tar xvpf v2.0-r2.tar.gz && \
    cd /data/install/srs-2.0-r2/trunk && \
    mkdir /data/install/srs-2.0-r2/trunk/objs && \
    cp /data/install/srs-2.0-r2/trunk/3rdparty/CherryPy-3.2.4.zip /data/install/srs-2.0-r2/trunk/objs/ && \
    cd /data/install/srs-2.0-r2/trunk/objs/ && \
    unzip CherryPy-3.2.4.zip && \
    cd /data/install/srs-2.0-r2/trunk/ && \
    ./configure && make -j16 && \
    cp -rL /data/install/srs-2.0-r2/trunk/objs/ffmpeg/ /usr/local/ && \
    cp -L /data/install/srs-2.0-r2/trunk/objs/srs /usr/local/bin/ && \
    cd /data && \
    rm -rf /data/install && \
    apt-get remove -y --force-yes --purge --auto-remove automake autoconf libtool build-essential wget ca-certificates unzip libpcre3-dev zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /data

CMD [ "/data/install/srs-2.0-r2/trunk/objs/srs", "-c conf/srs.conf" ]
