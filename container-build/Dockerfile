FROM ubuntu:bionic
RUN apt-get update
RUN apt-get install sudo

RUN adduser --disabled-password --gecos '' docker
RUN adduser docker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER docker
RUN sudo apt-get update 
RUN sudo apt-get install -y git wget flex bison gperf python python-pip python-setuptools cmake ninja-build ccache libffi-dev libssl-dev build-essential gawk texinfo tree squashfs-tools
RUN sudo mkdir -p /output/lfs /tools
ADD lfs-scripts /home/docker/scripts
RUN sudo chown -R docker /output /home/docker/scripts /tools
WORKDIR /home/docker/scripts
RUN bash version-check.sh
RUN bash -x 01-toolchain
RUN printf "==============\n--BUILD OUTPUT--\n"
RUN tree /output