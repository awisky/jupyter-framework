FROM jupyter/minimal-notebook:latest

USER root

# Update aptitude with new repo
RUN apt-get update \
    && apt-get install -y git

COPY ./requirements.txt ./

# Install Wget
RUN apt-get update && apt-get install -y --no-install-recommends wget

# Install Python3 and all the requirements.txt
RUN apt-get update && apt-get install -y --no-install-recommends \
        apt-utils \
        python3-dev \
        python3-wheel \
    && pip3 install --upgrade pip \
    && pip3 install -r requirements.txt
