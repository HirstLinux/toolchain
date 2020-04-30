FROM ubuntu:bionic
RUN apt-get update
RUN apt-get install sudo

RUN adduser --disabled-password --gecos '' docker
RUN adduser docker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER docker

RUN sudo apt-get update 
RUN sudo apt-get install git
COPY version-check.sh /
RUN chmod +x /version-check.sh
RUN bash /version-check.sh
