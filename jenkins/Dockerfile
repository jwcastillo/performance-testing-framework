FROM jenkins/jenkins:lts-slim-jdk21

# ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false -Dhudson.model.DirectoryBrowserSupport.CSP=''"
# COPY security.groovy /usr/share/jenkins/ref/init.groovy.d/security.groovy
# COPY configure-markup-formatter.groovy /usr/share/jenkins/ref/init.groovy.d/configure-markup-formatter.groovy
# COPY jobs/ /jobs/
# COPY run.sh /run.sh 
# COPY jenkins-cli.jar /jenkins-cli.jar
# COPY error_parsing /error_parsing
# COPY hudson.plugins.logparser.LogParserPublisher.xml /var/jenkins_home/hudson.plugins.logparser.LogParserPublisher.xml


USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli

USER jenkins
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
ENV PATH "$PATH:/usr/local/bin/dind/"