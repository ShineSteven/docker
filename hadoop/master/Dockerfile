FROM shinest/hadoop_slave:0.1
MAINTAINER Shine St <fan.steven.chiang@gmail.com>
RUN apt-get update && apt-get install -y \
scala && \
sed -i '$a export SCALA_HOME=/usr/share/scala' /home/hadoop/.bashrc

ENV SCALA_HOME /usr/share/scala

EXPOSE 4044 8080 8088

CMD ["/bin/bash"]
