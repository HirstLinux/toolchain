FROM hirstlinux/utility-image:2
USER docker
RUN sudo mkdir -p /output/lfs /output/lfs/tools
ADD lfs-scripts /home/docker/scripts
RUN sudo chown -R docker /output /home/docker/scripts /output/lfs/tools
WORKDIR /home/docker/scripts
RUN bash version-check.sh
CMD /bin/bash