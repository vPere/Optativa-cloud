FROM ubi7/ubi7:7.7
ENV PORT=8080
MAINTAINER Alex<atello@edu.tecnocampus.cat>
LABEL desc="Apache custom container" 
EXPOSE ${PORT}
RUN   yum install -y httpd &&\
      yum -y clean all --enablerepo='*' &&\
      sed -ri -e "/^Listen 80/c\Listen ${PORT}" /etc/httpd/conf/httpd.conf &&\
      echo "Hello from Dockerfile" > /var/www/html/index.html && \
      chown -R apache.apache /etc/httpd/logs &&\
      chown -R apache.apache /run/httpd 

ENTRYPOINT ["httpd", "-D", "FOREGROUND"]