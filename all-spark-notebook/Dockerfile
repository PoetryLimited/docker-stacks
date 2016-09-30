# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/pyspark-notebook

MAINTAINER Jupyter Project <jupyter@googlegroups.com>

USER root

# RSpark config
ENV R_LIBS_USER $SPARK_HOME/R/lib

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

# R packages
# Pin r-base to a specific build number for https://github.com/jupyter/docker-stacks/issues/210#issuecomment-246081809
RUN conda config --add channels r && \
    conda install --quiet --yes \
    'r-base=3.3.1 1' \
    'r-irkernel=0.6*' \
    'r-ggplot2=2.1*' \
    'r-rcurl=1.95*' && conda clean -tipsy

# Apache Toree kernel
RUN pip --no-cache-dir install toree==0.1.0.dev7
RUN jupyter toree install --user

# Install gradle
RUN wget https://services.gradle.org/distributions/gradle-3.1-bin.zip 
RUN apt-get install -y unzip
RUN unzip gradle-3.1-bin.zip 
RUN mv gradle-2.0 /opt/
RUN rm gradle-2.0-bin.zip
ENV GRADLE_HOME /opt/gradle-2.0
ENV PATH $PATH:$GRADLE_HOME/bin

# Add spark to path

# Install Airflow
