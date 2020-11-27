FROM centos/systemd
LABEL maintainer="fikolis@pm.me"
RUN yum update; yum -y install \
  which \
  gcc \
  glibc \
  glibc-common \
  wget \
  unzip \
  httpd \
  php \
  gd \
  gd-devel \
  perl \
  postfix \
  make \
  gettext \
  automake \ 
  autoconf \
  openssl-devel \
  net-snmp \
  net-snmp-utils \
  epel-release \
  perl-Crypt-DES \
  nmap-ncat && \
  yum clean all
WORKDIR /tmp
RUN wget -O nagioscore.tar.gz https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.4.5.tar.gz &&\
  tar xzf nagioscore.tar.gz && \
  cd nagioscore-nagios-4.4.5/ && \
  ./configure --&& \
  make all && \
  make install-groups-users &&\
  usermod -a -G nagios apache &&\
  make install && \
  make install-daemoninit &&\
  make install-commandmode && \
  make install-config &&\
  make install-webconf && \
  systemctl enable httpd.service && systemctl enable nagios.service && \ 
  /usr/bin/htpasswd -cb /usr/local/nagios/etc/htpasswd.users nagiosadmin "nagios" && \
  wget --no-check-certificate -O nagios-plugins.tar.gz https://github.com/nagios-plugins/nagios-plugins/archive/release-2.2.1.tar.gz && \
  tar zxf nagios-plugins.tar.gz && \
  cd nagios-plugins-release-2.2.1/ && \
  ./tools/setup && \
  ./configure && \
  make && \
  make install && \
  rm -rf /tmp/*
EXPOSE 80
CMD ["/usr/sbin/init"] 
