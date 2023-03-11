FROM jenkins/jenkins:2.387.1-lts

ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false -Dhudson.model.DirectoryBrowserSupport.CSP=''"
COPY security.groovy /usr/share/jenkins/ref/init.groovy.d/security.groovy
COPY configure-markup-formatter.groovy /usr/share/jenkins/ref/init.groovy.d/configure-markup-formatter.groovy
COPY jobs/ /jobs/
COPY run.sh /run.sh
COPY error_parsing /error_parsing
COPY hudson.plugins.logparser.LogParserPublisher.xml /var/jenkins_home/hudson.plugins.logparser.LogParserPublisher.xml
COPY plugins.txt /usr/share/jenkins/ref/

USER root
RUN jenkins-plugin-cli --plugins "greenballs"
RUN jenkins-plugin-cli --plugins "htmlpublisher"
RUN jenkins-plugin-cli --plugins "show-build-parameters"
RUN jenkins-plugin-cli --plugins "filesystem-list-parameter-plugin"
RUN jenkins-plugin-cli --plugins "git"
RUN jenkins-plugin-cli --plugins "rebuild"
RUN jenkins-plugin-cli --plugins "persistent-parameter"
RUN jenkins-plugin-cli --plugins "postbuild-task"
RUN jenkins-plugin-cli --plugins "parameter-separator"
RUN jenkins-plugin-cli --plugins "log-parser"
RUN jenkins-plugin-cli --plugins "compress-buildlog"
RUN jenkins-plugin-cli --plugins "groovy-postbuild"
RUN jenkins-plugin-cli --plugins "antisamy-markup-formatter"
RUN jenkins-plugin-cli --plugins "ssh-slaves"
RUN apt-get -y update && \
apt-get -y install sudo && \
sudo usermod -aG staff jenkins && \
echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
ENV PATH "$PATH:/usr/local/bin/dind/"

ENTRYPOINT ["bash","-x","/run.sh"]
