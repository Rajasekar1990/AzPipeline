FROM openjdk:8

MAINTAINER Rajasekar S <rajasekars792@gmail.com>

ENV JMETER_VERSION 5.4.3
ENV JMETER_HOME /jmeter/apache-jmeter-$JMETER_VERSION/
ENV PATH ${JMETER_HOME}/bin:${PATH}
ENV JMETER_PLUGINS ${JMETER_HOME}/lib/ext
ENV JMETER_PLUGINS_DOWNLOAD_URL https://repo1.maven.org/maven2/kg/apc

#Install Unix utilities
RUN apt-get clean && \
	apt-get update && \
	apt-get -qy install \
				wget \
				telnet \
				iputils-ping \
				unzip

# Install JMeter
RUN mkdir /jmeter && \
	cd /jmeter/ && \
	wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz && \
	tar -xzf apache-jmeter-${JMETER_VERSION}.tgz && \
	rm apache-jmeter-${JMETER_VERSION}.tgz

RUN wget https://repo1.maven.org/maven2/kg/apc/cmdrunner/2.2/cmdrunner-2.2.jar && \
  mv cmdrunner-2.2.jar ${JMETER_HOME}/lib/cmdrunner-2.2.jar

# Install Required Plugins
#Plugin Manager
RUN wget https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-manager/1.6/jmeter-plugins-manager-1.6.jar && \
  mv jmeter-plugins-manager-1.6.jar ${JMETER_PLUGINS}

RUN java -cp ${JMETER_PLUGINS}/jmeter-plugins-manager-1.6.jar org.jmeterplugins.repository.PluginManagerCMDInstaller

RUN ${JMETER_HOME}/bin/PluginsManagerCMD.sh status

RUN wget https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-cmn-jmeter/0.5/jmeter-plugins-cmn-jmeter-0.5.jar && \
  mv jmeter-plugins-cmn-jmeter-0.5.jar ${JMETER_PLUGINS}

RUN wget  https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-graphs-additional/2.0/jmeter-plugins-graphs-additional-2.0.jar && \
  mv jmeter-plugins-graphs-additional-2.0.jar ${JMETER_PLUGINS}

RUN wget https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-graphs-basic/2.0/jmeter-plugins-graphs-basic-2.0.jar && \
  mv jmeter-plugins-graphs-basic-2.0.jar ${JMETER_PLUGINS}

RUN wget https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-graphs-additional/2.0/jmeter-plugins-graphs-additional-2.0.jar && \
  mv jmeter-plugins-graphs-additional-2.0.jar ${JMETER_PLUGINS}

RUN wget https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-functions/2.0/jmeter-plugins-functions-2.0.jar && \
  mv jmeter-plugins-functions-2.0.jar ${JMETER_PLUGINS}

RUN wget https://repo1.maven.org/maven2/kg/apc/jmeter-plugins-tst/2.3/jmeter-plugins-tst-2.3.jar && \
  mv jmeter-plugins-tst-2.3.jar ${JMETER_PLUGINS}

#Random CSV plugin
RUN wget https://jmeter-plugins.org/files/packages/bzm-random-csv-0.6.zip && \
  unzip bzm-random-csv-0.6.zip && \
  mv lib/ext/jmeter-plugins-random-csv-data-set-0.6.jar ${JMETER_PLUGINS} && \
  mv lib/jmeter-plugins-cmn-jmeter-0.4.jar ${JMETER_PLUGINS}

#parallel plugin
RUN wget https://jmeter-plugins.org/files/packages/bzm-parallel-0.11.zip && \
  unzip bzm-parallel-0.11.zip && \
  mv lib/ext/jmeter-parallel-0.11.jar ${JMETER_PLUGINS} && \
  mv lib/jmeter-plugins-cmn-jmeter-0.4.jar ${JMETER_PLUGINS}

#Custom thread group plugin
RUN wget https://jmeter-plugins.org/files/packages/jpgc-casutg-2.9.zip && \
  unzip jpgc-casutg-2.9.zip && \
  mv lib/ext/jmeter-plugins-casutg-2.9.jar ${JMETER_PLUGINS} && \
  mv lib/jmeter-plugins-cmn-jmeter-0.6.jar ${JMETER_PLUGINS}

#Prometheus Listener plugin
RUN wget https://repo1.maven.org/maven2/com/github/johrstrom/jmeter-prometheus-plugin/0.6.0/jmeter-prometheus-plugin-0.6.0.jar && \
  mv jmeter-prometheus-plugin-0.6.0.jar ${JMETER_PLUGINS}

#WebDriver plugin
RUN wget https://jmeter-plugins.org/files/packages/jpgc-webdriver-3.3.zip && \
  unzip jpgc-webdriver-3.3.zip && \
  mv lib/ext/* ${JMETER_PLUGINS}

#Remove jar conflicts
RUN rm ${JMETER_PLUGINS}/jmeter-plugins-cmn-jmeter-0.4.jar
RUN rm ${JMETER_PLUGINS}/jmeter-plugins-cmn-jmeter-0.5.jar
RUN rm ${JMETER_PLUGINS}/jmeter-plugins-manager-1.4.jar
RUN rm ${JMETER_PLUGINS}/jmeter-plugins-manager-1.3.jar
RUN rm ${JMETER_PLUGINS}/jmeter-plugins-manager-0.20.jar

#List of all plugins installed
RUN ${JMETER_HOME}/bin/PluginsManagerCMD.sh status
RUN ${JMETER_HOME}/bin/PluginsManagerCMD.sh install jmeter-prometheus=0.6.0

#Add jmx and csv files to master and slave machines
COPY Pipeline_SampleScript.jmx ${JMETER_HOME}/bin/Pipeline_SampleScript.jmx

ENV PATH $PATH:$JMETER_BIN



	
