#################################################################
# Dockerfile
#
# Version:          1
# Software:         DIA-Umpire
# Software Version: 1.4256
# Description:      computational analysis of data independent acquisition (DIA) mass spectrometry-based proteomics data
# Website:          http://diaumpire.sourceforge.net
# Tags:             Proteomics
# Provides:         dia-umpire 1.4256
# Base Image:       biodckr/biodocker:latest
# Build Cmd:        docker build --rm -t biodckr/diaumpire 1.4256/.
# Pull Cmd:         docker pull biodckr/diaumpire
# Run Cmd:          docker run --rm biodckr/diaumpire [options]
#################################################################

# Set the base image
FROM biodckr/biodocker:latest

################## BEGIN INSTALLATION ###########################

USER root

RUN apt-get update && \
  apt-get install -y \
  gnuplot && \
  apt-get clean && \
  apt-get purge && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Installing TPP
RUN ZIP=tpp-4.8.0.zip && \
  mkdir -p /usr/local && \
  wget https://github.com/BioDocker/software-archive/releases/download/TPP/$ZIP -O /tmp/$ZIP && \
  unzip /tmp/$ZIP -d /usr/local && \
  rm /tmp/$ZIP

ENV PATH /usr/local/tpp/bin/:$PATH

# Installing DIA-Umpire
RUN ZIP=DIA-Umpire_v1_4256.zip && \
  wget https://github.com/BioDocker/software-archive/releases/download/DIA-Umpire/$ZIP -O /tmp/$ZIP && \
  unzip /tmp/$ZIP -d /home/biodocker/bin/DIA-Umpire/ && \
  chmod -R 755 /home/biodocker/bin/DIA-Umpire/ && \
  rm /tmp/$ZIP

ENV PATH /home/biodocker/bin/DIA-Umpire/:$PATH

# Installing Comet
RUN ZIP=comet_binaries_2015010.zip && \
  wget https://github.com/BioDocker/software-archive/releases/download/Comet/$ZIP -O /tmp/$ZIP && \
  unzip /tmp/$ZIP -d /home/biodocker/bin/comet/ && \
  rm /tmp/$ZIP && \
  chmod 755 /home/biodocker/bin/comet/*.exe && \
  ln -sv /home/biodocker/bin/comet/*.exe /home/biodocker/bin/

ENV PATH /home/biodocker/bin/comet/:$PATH

# Installing MSGF+
RUN ZIP=MSGFPlus_9949.zip && \
  wget https://github.com/BioDocker/software-archive/releases/download/MSGFPlus/$ZIP -O /tmp/$ZIP && \
  unzip /tmp/$ZIP -d /home/biodocker/bin/MSGFPlus/ && \
  chmod -R 755 /home/biodocker/bin/MSGFPlus/* && \
  rm /tmp/$ZIP

ENV PATH /home/biodocker/bin/MSGFPlus/:$PATH

USER biodocker

WORKDIR /data/

##################### INSTALLATION END ##########################

# File Author / Maintainer
MAINTAINER Felipe da Veiga Leprevost <felipe@leprevost.com.br>
# Modified by Felipe da Veiga Leprevost 01-26-2016
