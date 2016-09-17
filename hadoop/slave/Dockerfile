FROM ubuntu:16.04
MAINTAINER Shine St <fan.steven.chiang@gmail.com>
RUN apt-get update && apt-get install -y \
default-jdk \
ssh \
rsync

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

RUN mkdir /var/run/sshd && \
sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
echo 'root:roottest' | chpasswd

RUN useradd -ms /bin/bash hadoop && \
echo 'hadoop:hadooptest' | chpasswd && \
adduser hadoop sudo && \
su - hadoop -c 'mkdir /home/hadoop/.ssh' && \
sed -i '$a export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64' /home/hadoop/.bashrc

WORKDIR /tmp
COPY conf slave_conf
RUN wget -nv http://apache.stu.edu.tw/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz && \
tar -zxv -f hadoop-2.7.3.tar.gz && \
mv /tmp/hadoop-2.7.3 /usr/local/hadoop && \
rm -rf hadoop-2.7.3.tar.gz && \
cp /tmp/slave_conf/hadoop/* /usr/local/hadoop/etc/hadoop && \
chown -R hadoop:hadoop /usr/local/hadoop

EXPOSE 22 8042 50090

CMD ["/usr/sbin/sshd", "-D"]
