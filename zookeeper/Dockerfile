FROM tempoiq/java:7
MAINTAINER TempoIQ

ENV ZOOKEEPER_VER 3.4.6
ENV PATH /opt/exhibitor:$PATH

RUN apt-get update && \
    apt-get -y install ca-certificates && \
    wget -q http://archive.apache.org/dist/zookeeper/zookeeper-${ZOOKEEPER_VER}/zookeeper-${ZOOKEEPER_VER}.tar.gz.md5 && \
    wget -q http://archive.apache.org/dist/zookeeper/zookeeper-${ZOOKEEPER_VER}/zookeeper-${ZOOKEEPER_VER}.tar.gz && \
    md5sum -c zookeeper-${ZOOKEEPER_VER}.tar.gz.md5 && \
    tar xzf zookeeper-${ZOOKEEPER_VER}.tar.gz && \
    rm /zookeeper-${ZOOKEEPER_VER}.tar.gz* && \
    mv /zookeeper-${ZOOKEEPER_VER} /opt/zookeeper

RUN apt-get -y install maven && \
    mkdir /opt/exhibitor

WORKDIR /opt/exhibitor

VOLUME /opt/zookeeper/data

ADD pom.xml /opt/exhibitor/pom.xml

RUN mvn assembly:single && \
    mv target/exhibitor-1.0-jar-with-dependencies.jar . && \
    rm -rf /opt/exhibitor/target && \
    rm /opt/exhibitor/pom.xml

ADD exhibitor.properties /opt/exhibitor/exhibitor.properties
ADD exhibitor /opt/exhibitor/exhibitor

EXPOSE 2181 2888 3888 8080

ENTRYPOINT ["java", "-jar", "exhibitor-1.0-jar-with-dependencies.jar", "-c", "file"]
