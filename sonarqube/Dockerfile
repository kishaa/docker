FROM centos-jdk:8u212

MAINTAINER Kunal Mehta <kunal.c.mehta@outlook.com>

RUN yum install wget unzip -y

ENV SONAR_VERSION=7.7
ENV  SONARQUBE_HOME=/opt/sonarqube-${SONAR_VERSION}

ENV SONARQUBE_JDBC_USERNAME=
ENV SONARQUBE_JDBC_PASSWORD=
ENV SONARQUBE_JDBC_URL=

RUN groupadd -r sonarqube && useradd -r -g sonarqube sonarqube

RUN cd /opt && wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-${SONAR_VERSION}.zip && \
    unzip sonarqube-${SONAR_VERSION}.zip && rm -rf /opt/sonarqube-${SONAR_VERSION}.zip

RUN chmod 0666 /opt/sonarqube-${SONAR_VERSION}/conf/sonar.properties && \
    mv /opt/sonarqube-$SONAR_VERSION /opt/sonarqube && \
    chown -R sonarqube:sonarqube /opt/sonarqube/

# Http port
EXPOSE 9000

VOLUME "$SONARQUBE_HOME/data"

WORKDIR $SONARQUBE_HOME

COPY run.sh $SONARQUBE_HOME/bin/
RUN chmod 777 $SONARQUBE_HOME/bin/run.sh

USER root

ENTRYPOINT ["./bin/run.sh"]
