FROM centos:7

MAINTAINER ZomboDB, LLC (zombodb@gmail.com)

RUN yum update -y
RUN yum install -y openssl
RUN yum install -y http://yum.postgresql.org/9.3/redhat/rhel-6-x86_64/pgdg-redhat93-9.3-3.noarch.rpm
RUN yum install -y postgresql93-devel
RUN yum install -y gcc make zlib-devel

COPY curl-7.53.1.tar.gz /usr/local/src/
WORKDIR /usr/local/src/
RUN tar xzf curl-7.53.1.tar.gz
WORKDIR /usr/local/src/curl-7.53.1/
RUN ./configure --without-ssl \
   --disable-threaded-resolver \
   --disable-dict \
   --disable-file \
   --disable-ftp \
   --disable-gopher \
   --disable-imap \
   --disable-pop3 \
   --disable-rtsp \
   --disable-smb \
   --disable-smtp \
   --disable-telnet \
   --disable-tftp
RUN make -j2 && make install
RUN ldconfig && ldconfig
RUN rm -rf /usr/local/src/curl*

ARG user
ARG uid
RUN useradd -ms /bin/bash --uid $uid $user
USER $user
ENV PATH /usr/pgsql-9.3/bin:$PATH
ENV IS_DOCKER true
