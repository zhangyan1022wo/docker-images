FROM 10.100.21.59:5000/oraclejdk8:apline
MAINTAINER Berrygenomics:20190530
ENV LANG C.UTF-8
ENV VERSION=8.5.6
ENV CATALINA_HOME=/opt/tomcat8
ENV PATH=$CATALINA_HOME/bin:$PATH

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN apk update && apk upgrade
RUN apk add --no-cache --virtual=build-dependencies wget openssl
RUN apk add --no-cache bash bash-doc bash-completion
RUN apk add --no-cache tzdata 
RUN wget http://archive.apache.org/dist/tomcat/tomcat-8/v${VERSION}/bin/apache-tomcat-${VERSION}.tar.gz \
&& tar zxf apache-tomcat-${VERSION}.tar.gz \
&& mv apache-tomcat-${VERSION} $CATALINA_HOME \
&& apk del build-dependencies \
&& rm -rf apache-tomcat-${VERSION}.tar.gz $CATALINA_HOME/webapps/* $CATALINA_HOME/bin/*.bat 
#&& sed -i "s#securerandom.source=file:/dev/random#securerandom.source=file:/dev/./urandom#g" $JAVA_HOME/jre/lib/security/java.security
 
WORKDIR $CATALINA_HOME
EXPOSE 8080
CMD ["catalina.sh", "run"]
