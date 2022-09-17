# Use jmbase Docker base image
#FROM rajasekars792/jmbaseimage:latest
FROM jmeteracrrepo.azurecr.io/jmeter:jmeter5.3Azmasterv1

MAINTAINER Rajasekar S <rajasekars792@gmail.com>

#ENV JMETER_VERSION 5.4.3
#ENV JMETER_HOME /jmeter/apache-jmeter-$JMETER_VERSION/

ENV JMETER_VERSION 5.3
ENV JMETER_HOME /home/jmeter/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN $JMETER_HOME/bin
ENV JMETER_PLUGINS ${JMETER_HOME}/lib/ext
ENV JMETER_PLUGINS_DOWNLOAD_URL https://repo1.maven.org/maven2/kg/apc
ENV PATH ${JMETER_HOME}/bin:${PATH}

# Ports to be exposed from the container for JMeter Slaves
EXPOSE 1099 50000

ENV PATH $PATH:$JMETER_BIN
WORKDIR $JMETER_HOME

# Application to run on starting the container
ENTRYPOINT ${JMETER_HOME}/bin/jmeter-server \
                        -Dserver.rmi.localport=50000 \
                        -Dserver_port=1099 \
                        -Jserver.rmi.ssl.disable=true