FROM centos:7
# version 22.0

#MAINTAINER MW1-4@tamx.co.kr

# 0) Install necessary packages through yum in CentOS
RUN set -eux; \
    yum update -y; \
    yum install -y \
        make \
        gcc \
        gcc-c++ \
        perl \
	wget \
        libxslt-devel \
        ca-certificates \
    ; \rm -rf /var/lib/apt/lists/*

# 1) Nginx env set
ENV SOURCE_PATH /usr/local/src
ENV NGINX_PREFIX /usr/local/nginx
ENV NGINX_CONF_PATH $NGINX_PREFIX/conf
ENV SSL_PATH $NGINX_PREFIX/ssl
ENV LICENSE_PATH $NGINX_PREFIX/license

ENV LIBRARY_DOWNLOAD_PATH https://github.com/TmaxSoftOfficial/HyperFrame-Nginx-Image/raw/master/lib

ENV ZLIB_VERSION 1.2.11
ENV PCRE_VERSION 8.45
ENV OPENSSL_VERSION 1.1.1l
ENV NGINX_MAJOR_VERSION 1.20
ENV NGINX_MINOR_VERSION 1

ENV NGINX_PORT 80
ENV SSL_PORT 443

# environment PATH set
ENV PATH $NGINX_PREFIX/sbin:$NGINX_PREFIX:$PATH

# 2) copy sample_key to use OpenSSL
COPY ./ssl/server.crt $SSL_PATH/
COPY ./ssl/server.key $SSL_PATH/
# copy shell script to set password for OpenSSL sample_key
COPY ./ssl/ssl_passwd $SSL_PATH/
# comment out 2) if you do not want to use OpenSSL

# copy start.sh to run Nginx
COPY ./start.sh $NGINX_PREFIX/

# copy Nginx license
COPY ./license/ $LICENSE_PATH

# 3) library build
# 3_1) zlib
RUN set -eux; \
    cd $SOURCE_PATH; \
    wget $LIBRARY_DOWNLOAD_PATH/zlib-${ZLIB_VERSION}.tar.gz; \
    tar -zxvf zlib-${ZLIB_VERSION}.tar.gz

# 3_2) PCRE
RUN set -eux; \
    cd $SOURCE_PATH; \
    wget $LIBRARY_DOWNLOAD_PATH/pcre-${PCRE_VERSION}.tar.gz; \
    tar -zxvf pcre-${PCRE_VERSION}.tar.gz

# 3_3) OpenSSL
RUN set -eux; \
    cd $SOURCE_PATH; \ 
    wget $LIBRARY_DOWNLOAD_PATH/openssl-${OPENSSL_VERSION}.tar.gz; \
    tar -zxvf openssl-${OPENSSL_VERSION}.tar.gz

# 3_4) Nginx
RUN set -eux; \
    cd $SOURCE_PATH; \  
    wget $LIBRARY_DOWNLOAD_PATH/nginx-${NGINX_MAJOR_VERSION}.${NGINX_MINOR_VERSION}.tar.gz; \
    tar -zxvf nginx-${NGINX_MAJOR_VERSION}.${NGINX_MINOR_VERSION}.tar.gz; \
    cd nginx-${NGINX_MAJOR_VERSION}.${NGINX_MINOR_VERSION}; \ 
    ./configure \
        --prefix=$NGINX_PREFIX \
        --with-zlib=$SOURCE_PATH/zlib-${ZLIB_VERSION} \
        --with-pcre=$SOURCE_PATH/pcre-${PCRE_VERSION} \
        --with-openssl=$SOURCE_PATH/openssl-${OPENSSL_VERSION} \
        --with-http_ssl_module \
        --with-http_v2_module \
    ; \
    # source-based compilation and generate installation binaries
    make; \
    make install

RUN set -eux; \
    rm -rf $SOURCE_PATH/*; \
    \
    # permission settings
    chmod 755 $NGINX_PREFIX/start.sh; \
    \
    # Nginx version check
    nginx -v

# 4) copy configuration file
COPY ./conf/nginx.conf $NGINX_CONF_PATH/nginx.conf
# DocumentRoot in nginx.conf : "/"

# http port number: 80 https port number : 443
EXPOSE 80 443

# run Nginx
CMD start.sh


