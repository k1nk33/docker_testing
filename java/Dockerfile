FROM k1:base


MAINTAINER 'k1nk33'

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" >> /etc/apt/sources.list && \
  TMPNAME=$(tempfile) && \
  apt-get update >> /dev/null 2> $TMPNAME && \
  PGPKEY=`cat $TMPNAME | cut -d":" -f6 | cut -d" " -f3` && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys $PGPKEY && \
  rm $TMPNAME && \
  apt-get update && \
  echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y oracle-java7-installer oracle-java7-set-default

ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
RUN echo "export JAVA_HOME=/usr/lib/jvm/java-7-oracle" >> ~/.bashrc

#Clean up apt-repository
RUN apt-get clean && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
