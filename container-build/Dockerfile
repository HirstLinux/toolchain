FROM hirstlinux/utility-image:2
USER docker
RUN sudo mkdir -p /output/lfs /output/lfs/tools
ADD lfs-scripts /home/docker/scripts
RUN sudo ln -s /output/lfs/tools /tools
RUN sudo chown -R docker /output /home/docker/scripts /tools
WORKDIR /home/docker/scripts
RUN bash version-check.sh
RUN bash -x 01-toolchain
RUN printf "==============\n--BUILD OUTPUT--\n"
RUN tree /output