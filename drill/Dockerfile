FROM tempoiq/java:7
MAINTAINER TempoIQ

ENV DRILL_VER 1.2.0

RUN apt-get install -y wget tar

RUN wget -q http://getdrill.org/drill/download/apache-drill-${DRILL_VER}.tar.gz && \
    tar xzf apache-drill-${DRILL_VER}.tar.gz && \
    rm /apache-drill-${DRILL_VER}.tar.gz* && \
    mv /apache-drill-${DRILL_VER} /opt/drill

ADD drill-env.sh /opt/drill/conf/drill-env.sh

WORKDIR /opt/drill

EXPOSE 8047 31010 31011 31012 46655

CMD /opt/drill/bin/drillbit.sh start && tail -f /opt/drill/log/drillbit.out
