FROM ubuntu:latest

# OS update and package installation process
RUN apt update \
  && apt-get -y install openjdk-8-jdk wget \
  && mkdir /usr/local/tomcat \
  && wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.43/bin/apache-tomcat-9.0.43.tar.gz -O /tmp/tomcat.tar.gz \
  && cd /tmp && tar xvfz tomcat.tar.gz \
  && mv /tmp/apache-tomcat-9.0.43 /tmp/tomcat
  && cp -Rv /tmp/tomcat/* /usr/local/tomcat/ \
  && rm -rf /tmp/tomcat \
  # Cleanup apt
  ###
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /usr/local/tomcat
# Copy tomcat users file to destination
# username: tomcat
# password: s3cr3t
#default role: manager-gui, manager-script
COPY settings/tomcat-users.xml /usr/local/tomcat/conf/tomcat-users.xml
COPY settings/context.xml /usr/local/tomcat/webapps/manager/META-INF/context.xml
COPY settings/manager.xml /usr/local/tomcat/conf/manager.xml

#Add an application to tomcat from your location to the container.
#ADD sample.war /usr/local/tomcat/webapps/

EXPOSE 8080
CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]

