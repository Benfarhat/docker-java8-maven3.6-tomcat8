# Ubuntu image
#
# Version 0.1

# Pull from Ubuntu


FROM wmarinho/ubuntu:oracle-jdk-7

MAINTAINER Wellington Marinho wpmarinho@globo.com

RUN DEBIAN_FRONTEND=noninteractive apt-get -y update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget pwgen curl

ENV TOMCAT_VERSION=8.0.8 \
    JAVA_HOME=/usr/lib/jvm/java-8-oracle \
    CATALINA_HOME=/tomcat \
    MAVEN_VERSION=3.6.0 \
    MAVEN_HOME=/usr/share/maven


# INSTALL JAVA
RUN \
  sudo echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90forceyes \
  && sudo echo 'APT::Get::force-yes "true";' >> /etc/apt/apt.conf.d/90forceyes \
  && sudo add-apt-repository ppa:openjdk-r/ppa \
  && sudo apt-get -y update \
  && sudo apt install -y openjdk-8-jre-headless \
  && sudo apt install -y openjdk-8-jdk

# INSTALL MAVEN
RUN mkdir -p /usr/share/maven \
  && wget https://www-us.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz -O maven.tar.gz\
  && tar -xvzf maven.tar.gz -C /usr/share/maven/ --strip-components=1 && rm maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

# INSTALL TOMCAT
RUN wget http://archive.apache.org/dist/tomcat/tomcat-8/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz -O tomcat.tar.gz
RUN tar zxf tomcat.tar.gz && rm tomcat.tar.gz && mv apache-tomcat* tomcat

ADD create_tomcat_admin_user.sh /create_tomcat_admin_user.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

EXPOSE 8080
CMD ["/run.sh"]

