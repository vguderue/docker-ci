#
# Creates a docker container with SonarQube, incl. several plugins
#

FROM sonarqube

# Set the JAVA_HOME variable to make it clear where Java is located
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0

ENV SONARQUBE_HOME /opt/sonarqube

# Plugin Versions
ENV SONAR_JAVA_PLUGIN 4.2
ENV SONAR_WEB_PLUGIN 2.4
ENV SONAR_SCM_GIT_PLUGIN 1.0

RUN INSTALL_PKGS="java-1.8.0-openjdk.x86_64" && \
    yum -y --setopt=tsflags=nodocs install $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all  && \
    localedef -f UTF-8 -i en_US en_US.UTF-8

# Http port
EXPOSE 9000

# H2 Database port
EXPOSE 9092

# Add plugins
RUN mkdir -p $SONARQUBE_HOME/extensions/plugins/
ADD http://central.maven.org/maven2/org/sonarsource/java/sonar-java-plugin/${SONAR_JAVA_PLUGIN}/sonar-java-plugin-${SONAR_JAVA_PLUGIN}.jar $SONARQUBE_HOME/extensions/plugins/sonar-java-plugin-${SONAR_JAVA_PLUGIN}.jar
ADD http://central.maven.org/maven2/org/sonarsource/sonar-web-plugin/sonar-web-plugin/${SONAR_WEB_PLUGIN}/sonar-web-plugin-${SONAR_WEB_PLUGIN}.jar $SONARQUBE_HOME/extensions/plugins/sonar-web-plugin-${SONAR_WEB_PLUGIN}.jar
ADD http://central.maven.org/maven2/org/codehaus/sonar-plugins/sonar-scm-git-plugin/${SONAR_SCM_GIT_PLUGIN}/sonar-scm-git-plugin-${SONAR_SCM_GIT_PLUGIN}.jar $SONARQUBE_HOME/extensions/plugins/sonar-scm-git-plugin-${SONAR_SCM_GIT_PLUGIN}.jar
COPY run.sh $SONARQUBE_HOME

WORKDIR $SONARQUBE_HOME

VOLUME ["$SONARQUBE_HOME/data","$SONARQUBE_HOME/conf","$SONARQUBE_HOME/logs"]

RUN chmod -R 777 $SONARQUBE_HOME

CMD ["/opt/sonarqube/run.sh"]
