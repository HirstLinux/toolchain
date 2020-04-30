FROM ubuntu:bionic
RUN apt-get update
RUN apt-get install sudo

RUN adduser --disabled-password --gecos '' docker
RUN adduser docker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER docker
RUN cd /home/docker
RUN sudo apt-get update 
RUN sudo apt-get install -y git wget flex bison gperf python python-pip python-setuptools cmake ninja-build ccache libffi-dev libssl-dev build-essential gawk texinfo
COPY version-check.sh /home/docker/
RUN sudo chmod +x /home/docker/version-check.sh
RUN sudo chown -R docker /home/docker
RUN bash /home/docker/version-check.sh
