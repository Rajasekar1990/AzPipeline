# Use jmbase Docker base image
FROM rajasekars792/jmbaseimage:latest

MAINTAINER Rajasekar S <rajasekars792@gmail.com>

ENV JMETER_VERSION 5.4.3
ENV JMETER_HOME /jmeter/apache-jmeter-$JMETER_VERSION/

# Ports to be exposed from the container for JMeter Slaves
EXPOSE 1099 50000

# Application to run on starting the container
ENTRYPOINT ${JMETER_HOME}/bin/jmeter-server \
                        -Dserver.rmi.localport=50000 \
                        -Dserver_port=1099 \
                        -Jserver.rmi.ssl.disable=true