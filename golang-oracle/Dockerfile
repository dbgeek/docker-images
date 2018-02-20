FROM oraclelinux:7-slim

ENV LD_LIBRARY_PATH /usr/lib/instantclient_12_2
ENV ORACLE_HOME /usr/lib/instantclient_12_2
ENV PATH=$PATH:/usr/local/go/bin
ENV PKG_CONFIG_PATH /usr/lib/pkgconfig
ENV GOPATH /src
ENV TNS_ADMIN /usr/lib/instantclient_12_2/network/admin

RUN yum -y install gzip tar pkg-config libaio git gcc && \
    yum clean all && \
		rm -rf /var/cache/yum && \
    curl -s -O https://dl.google.com/go/go1.9.4.linux-amd64.tar.gz && \
    tar -C /usr/local/ -xzf go1.9.4.linux-amd64.tar.gz && \
    rm -f go1.9.4.linux-amd64.tar.gz

COPY ./lib/oracle/instantclient_12_2 /usr/lib/instantclient_12_2
COPY ./lib/oracle/oci8.pc /usr/lib/pkgconfig/oci8.pc