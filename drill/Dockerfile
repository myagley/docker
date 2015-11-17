FROM java:7-jre
MAINTAINER TempoIQ

ENV DRILL_VER 1.2.0

RUN apt-get install -y wget tar

RUN mkdir -p /opt/software
RUN wget http://getdrill.org/drill/download/apache-drill-${DRILL_VER}.tar.gz -P /opt/software

RUN mkdir -p /usr/local/drill
RUN groupadd -r drill && useradd -d /home/drill -m -r -g drill drill
RUN chown drill:drill /usr/local/drill

USER drill

RUN tar -xvzf /opt/software/apache-drill-${DRILL_VER}.tar.gz -C /usr/local/drill
WORKDIR /usr/local/drill/apache-drill-${DRILL_VER}

ENTRYPOINT ["bin/drill-embedded"]
