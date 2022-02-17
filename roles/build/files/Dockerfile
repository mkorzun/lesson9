
FROM maven:3.8.4-jdk-8 AS build
RUN git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git /tmp/boxfuse-sample-java-war-hello-war-hello
RUN mvn -f /tmp/boxfuse-sample-java-war-hello-war-hello/pom.xml clean package
FROM alpine:latest
RUN set -x \
 && apk update \
 && apk add  --no-cache --virtual .checksum-deps \
      openjdk8-jre-base \
      wget
RUN set -x \
  && mkdir /opt/tomcat \
  && wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.75/bin/apache-tomcat-8.5.75.tar.gz \
  && tar xvzf apache-tomcat-8.5.75.tar.gz  --strip-components 1 --directory /opt/tomcat \
  && rm -rf apache-tomcat-8.5.75.tar.gz
COPY --from=build /tmp/boxfuse-sample-java-war-hello-war-hello/target/hello-*.war /opt/tomcat/webapps/
CMD ["/opt/tomcat/bin/catalina.sh", "run"]