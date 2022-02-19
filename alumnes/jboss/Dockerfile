FROM registry.access.redhat.com/ubi7:7.7
MAINTAINER Alex<atello@edu.tecnocampus.cat>
LABEL desc="Jboss custom container" 

ENV JBOSS_HOME="/opt/jboss"

EXPOSE 8080
EXPOSE 9090
EXPOSE 9990

COPY ./jboss-eap-7.2.0.zip /opt

RUN useradd jboss &&\
    usermod --password $RANDOM jboss &&\
    usermod -a -G wheel jboss &&\
    yum install -y java &&\
    yum install -y unzip &&\
    yum -y clean all --enablerepo='*'&&\
    unzip /opt/jboss-eap-7.2.0.zip -d /opt/jboss-eap-7.2.0 &&\
    mv -v /opt/jboss-eap-7.2.0/* ${JBOSS_HOME} &&\
    ${JBOSS_HOME}/bin/add-user.sh admin admin123 &&\
    echo \"JAVA_OPT=\"\$JAVA_OPTS -Djboss.bind.address=0.0.0.0 -	Djboss.bind.address.mnagement=0.0.0.0\"\">> /opt/jboss/bin/standalone.conf &&\
    chown -R jboss:0 ${JBOSS_HOME} 

USER jboss
CMD ["/opt/jboss/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
