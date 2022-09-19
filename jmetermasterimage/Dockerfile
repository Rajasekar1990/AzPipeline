FROM openjdk:8

MAINTAINER Rajasekar S <rajasekars792@gmail.com>

RUN useradd --create-home -s /bin/bash jmeter
WORKDIR /home/jmeter
USER jmeter

ENV JMETER_VERSION 5.3
ENV JMETER_HOME /home/jmeter/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN $JMETER_HOME/bin
ENV JMETER_PLUGINS ${JMETER_HOME}/lib/ext
ENV JMETER_PLUGINS_DOWNLOAD_URL https://repo1.maven.org/maven2/kg/apc
ENV PATH ${JMETER_HOME}/bin:${PATH}

RUN cd /tmp && \
    wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz && \
    tar -xzf apache-jmeter-${JMETER_VERSION}.tgz -C /home/jmeter

RUN wget https://repo1.maven.org/maven2/kg/apc/cmdrunner/2.2/cmdrunner-2.2.jar && \
  mv cmdrunner-2.2.jar ${JMETER_HOME}/lib/cmdrunner-2.2.jar

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

#Azure Backend Listener plugin
RUN wget https://jmeter-plugins.org/files/packages/jmeter.backendlistener.azure-0.2.8.zip && \
  unzip jmeter.backendlistener.azure-0.2.8.zip && \
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

ENV PATH $PATH:$JMETER_BIN
WORKDIR $JMETER_HOME
EXPOSE 9270 60000
CMD ["jmeter"]