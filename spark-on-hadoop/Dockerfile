# Dockerfile
FROM ubuntu:20.04 AS hadoop

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
 && apt-get install -y openjdk-8-jre curl python3 python3-pip \
 && rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"

# Install Apache Hadoop from Apache archives
RUN curl -L https://archive.apache.org/dist/hadoop/common/hadoop-3.2.3/hadoop-3.2.3.tar.gz \
  | tar -xzC /opt
WORKDIR /opt/hadoop-3.2.3


FROM hadoop AS jupyter

# Install miniconda for packing environments
RUN curl -L https://repo.anaconda.com/miniconda/Miniconda3-py39_4.11.0-Linux-x86_64.sh -o conda.sh \
  && bash ./conda.sh -b -u -p /opt/conda \
  && rm conda.sh

# Install Jupyter notebook
RUN pip install --no-cache-dir --upgrade pip \
 && pip install --no-cache-dir notebook

WORKDIR /app

ENTRYPOINT [ "jupyter", "notebook", "--ip=0.0.0.0" , "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''" ]
