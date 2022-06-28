ARG UBUNTU="20.04"

FROM ubuntu:${UBUNTU}

RUN sed -i 's@archive.ubuntu.com@mirror.kakao.com@g' /etc/apt/sources.list

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul
RUN apt-get update && apt-get install -y tzdata
RUN apt-get install -y net-tools wget nano openjdk-8-jdk openssh-server openssh-client iputils-ping

#Install ssh pdsh
ENV PDSH_RCMD_TYPE=ssh
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_dsa
RUN cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
RUN chmod 0600 ~/.ssh/authorized_keys

#Install java
ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
ENV PATH=$JAVA_HOME/bin/:$PATH

#Install hadoop
RUN mkdir workspace
RUN cd /workspace && wget https://archive.apache.org/dist/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz
RUN cd /workspace && tar -xvf hadoop-3.2.1.tar.gz
RUN cd /workspace && mv hadoop-3.2.1 hadoop

#hadoop config
RUN export HADOOP_HOME=/workspace/hadoop
RUN export HADOOP_CONFIG_HOME=$HADOOP_HOME/etc/hadoop
RUN export HADOOP_INSTALL=$HADOOP_HOME
RUN export HADOOP_MAPRED_HOME=$HADOOP_HOME
RUN export HADOOP_COMMON_HOME=$HADOOP_HOME
RUN export HADOOP_HDFS_HOME=$HADOOP_HOME
RUN export YARN_HOME=$HADOOP_HOME
RUN export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
RUN export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
RUN export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"

#hadoop user 
RUN export HDFS_NAMENODE_USER="root"
RUN export HDFS_DATANODE_USER="root"
RUN export HDFS_SECONDARYNAMENODE_USER="root"
RUN export YARN_RESOURCEMANAGER_USER="root"
RUN export YARN_NODEMANAGER_USER="root"