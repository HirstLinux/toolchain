# toolchain (HirstLinux)

Toolchain for building hirstlinux inside a container.

The inspiration for this project came from @emmett1's lfs-scripts project which used the Crux Linux package manager to build a LFS system. (https://github.com/emmett1/lfs-scripts)

This project will include a broad selection of packages and will be using the ArchLinux package manager pacman. 

#### Build Requirements

This toolchain is built within the hirstlinux/utility-image docker container. (https://github.com/hirstlinux/utility-image)

A Jenkinsfile is also included here for ease of building under Jenkins CI via dind (Docker-in-Docker).

#### Contributing
Contributions are certainly welcome; feel free to submit an issue or PR! I'm very open to design changes as this is mainly an educational project at this point.

#### License

All packages used here are licensed under their various licenses and any modifications or additions made in this project shall be licensed under the GPLv3 license.

#### Notes

This is very much still a work in progress. 

This project will be split into multiple repositories for differing purposes and is intended to become a base which can be easily used for custom distributions and lightweight systems.