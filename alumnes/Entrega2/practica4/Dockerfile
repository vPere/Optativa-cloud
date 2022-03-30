FROM ubi7/ubi:7.7
LABEL mantainer=Pere<pvidiella@edu.tecnocampus.cat>
ENV JBOSS_HOME="/opt/jboss"
LABEL description="JBOSS container vpere"

COPY ../jboss-eap-7.2.0.zip /opt

RUN useradd jboss &&\
    usermod --password $RANDOM jboss &&\
    usermod -aG wheel jboss &&\
    yum install -y unzip &&\
    yum install -y java &&\
    yum -y clean all &&\
    unzip /opt/jboss-eap-7.2.0.zip -d /opt &&\
    mv /opt/jboss-eap-7.2 ${JBOSS_HOME} &&\
    ${JBOSS_HOME}/bin/add-user.sh admin admin123 -s &&\
    echo 'JAVA_OPT="$JAVA_OPTS -Djboss.bind.address=0.0.0.0 -   Djboss.bind.address.mnagement=0.0.0.0"'>> ${JBOSS_HOME}/bin/standalone.conf

EXPOSE 8080
EXPOSE 9090
EXPOSE 9990    

RUN chown -R jboss:0 ${JBOSS_HOME}

USER jboss
CMD ["/opt/jboss/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]