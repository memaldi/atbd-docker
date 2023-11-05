FROM eclipse-temurin:8-alpine

WORKDIR /
RUN wget https://dlcdn.apache.org/flume/1.11.0/apache-flume-1.11.0-bin.tar.gz
RUN tar -xf apache-flume-1.11.0-bin.tar.gz
RUN rm apache-flume-1.11.0-bin.tar.gz

ENTRYPOINT ["/apache-flume-1.11.0-bin/bin/flume-ng", "agent", "start", "--name a1", "--conf-file", "/apache-flume-1.11.0-bin/flume.conf", "--conf", "/apache-flume-1.11.0-bin/conf"]

