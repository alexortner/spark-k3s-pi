FROM ubuntu:21.04

ENV hadoop_ver 3.3.0
ENV hadoop_url https://downloads.apache.org/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
ENV hadoop_file hadoop-3.3.0

ENV spark_ver 3.0.1
ENV spark_url https://downloads.apache.org/spark/spark-3.0.1/spark-3.0.1-bin-hadoop3.2.tgz
ENV spark_file spark-3.0.1-bin-hadoop3.2

# neceary to supress dialog on apt-get install
ENV DEBIAN_FRONTEND=noninteractive 

# Install OpenJDK 8
RUN apt-get update && \
    apt-get install -y apt-utils curl wget openjdk-8-jdk python3-pip python-dev build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Download Hadoop and install it in /opt/hadoop
RUN mkdir -p /opt && \
    cd /opt && \
    wget ${hadoop_url} && \
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