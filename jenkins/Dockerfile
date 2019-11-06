FROM registry.access.redhat.com/openshift3/jenkins-2-rhel7

ADD config-cloud.xml credentials.xml /opt/openshift/

# Install additional plugins and modify files
RUN mkdir -p /opt/openshift/plugins && \
          cat /opt/openshift/credentials.xml > /opt/openshift/configuration/credentials.xml && \
		  sed -i "s|<slaveAgentPort>.*</slaveAgentPort>|<slaveAgentPort>50000</slaveAgentPort>|" "/opt/openshift/configuration/config.xml.tpl" && \
		  sed -i "s|<numExecutors>.*</numExecutors>|<numExecutors>0</numExecutors>|" "/opt/openshift/configuration/config.xml.tpl" && \
		  sed -i "/<slaves\/>/r /opt/openshift/config-cloud.xml" "/opt/openshift/configuration/config.xml.tpl" && \
		  chmod -R og+rw /opt/openshift/plugins && \
		  rm -rf /opt/openshift/config-cloud.xml /opt/openshift/credentials.xml
