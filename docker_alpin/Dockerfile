FROM alpine:3.7

ENV hadoop_ver 3.3.0
ENV hadoop_url https://downloads.apache.org/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
ENV hadoop_file hadoop-3.3.0

ENV spark_ver 3.0.1
ENV spark_url https://downloads.apache.org/spark/spark-3.0.1/spark-3.0.1-bin-hadoop3.2.tgz
ENV spark_file spark-3.0.1-bin-hadoop3.2

 

# Install OpenJDK 8
RUN apk add --update \
    python3 \
    python3-dev \
    py-pip \
    build-base \
    openjdk8-jre \
    bash \
  && rm -rf /var/cache/apk/*

# Download Hadoop and install it in /opt/hadoop
RUN mkdir -p /opt && \
    cd /opt && \
    wget --quiet ${hadoop_url} && \
    tar -xf ${hadoop_file}.tar.gz && \
    ln -s ${hadoop_file} hadoop && \
    rm ${hadoop_file}.tar.gz && \
    echo Hadoop ${hadoop_ver} libraries installed in /opt/hadoop/

# Download Spark and install it in /opt/spark
RUN mkdir -p /opt && \
    cd /opt && \
    wget ${spark_url} && \
    tar -xf ${spark_file}.tgz && \
    ln -s ${spark_file} spark && \
    rm ${spark_file}.tgz && \
    echo Spark ${spark_ver}  installed in /opt/spark/

ADD log4j.properties /opt/spark/conf/log4j.properties
ADD start-common.sh start-worker start-master /
ADD core-site.xml /opt/spark/conf/core-site.xml
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf
ENV PATH $PATH:/opt/spark/bin
