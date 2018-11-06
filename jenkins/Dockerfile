FROM bxvip/androidenv:v1.0
MAINTAINER vic "bxvipsky@gmail.com"

WORKDIR ${USR_LOCAL}

ENV JENKINS_UC https://updates.jenkins-ci.org
ENV COPY_REFERENCE_FILE_LOG /var/log/copy_reference_file.log
RUN useradd -d "${JENKINS_HOME}" -u 1000 -m -s /bin/bash jenkins
RUN mkdir -p /usr/share/jenkins/ref/init.groovy.d
COPY /etc/scripts/init.groovy /usr/share/jenkins/ref/init.groovy.d/tcp-slave-agent-port.groovy
RUN curl -fL http://mirrors.jenkins-ci.org/war-stable/$JENKINS_VERSION/jenkins.war -o /usr/share/jenkins/jenkins.war && \
    chown -R jenkins "${JENKINS_HOME}" /usr/share/jenkins/ref && \
    touch $COPY_REFERENCE_FILE_LOG && chown jenkins.jenkins $COPY_REFERENCE_FILE_LOG
COPY /etc/scripts/jenkins.sh /usr/local/bin/jenkins.sh
RUN chmod a+x /usr/local/bin/jenkins.sh
VOLUME ${JENKINS_HOME}
EXPOSE 8080

# Copy start script
COPY /etc/scripts/start.sh /usr/local/start.sh
RUN chmod a+x /usr/local/start.sh
