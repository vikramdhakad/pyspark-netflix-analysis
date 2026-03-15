# Base image
FROM python:3.10-bullseye

# Install Java (required for Spark)
RUN apt-get update && apt-get install -y openjdk-17-jdk wget

# Set Java Home
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$PATH:$JAVA_HOME/bin

# Install Spark
ENV SPARK_VERSION=3.5.0
ENV HADOOP_VERSION=3

RUN wget https://archive.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz \
    && tar -xzf spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz \
    && mv spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION /opt/spark \
    && rm spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz

ENV SPARK_HOME=/opt/spark
ENV PYTHONPATH=$SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.9.7-src.zip
ENV PATH=$SPARK_HOME/bin:$PATH

# Set Spark environment 
ENV SPARK_HOME=/opt/spark
ENV PATH=$PATH:SPARK_HOME/bin

# Install PySpark & Jupyter 
RUN pip install pyspark jupyter pandas

# Working directory
WORKDIR /app

# Expose Jupyter port
EXPOSE 8888

# Start Jupyter Notebook
CMD ["jupyter","notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root"]
