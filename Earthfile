VERSION 0.7

image:
    ARG distribution="bullseye"
    FROM debian:${distribution}

    ENV DEBIAN_FRONTEND=noninteractive

    RUN apt update -y
    RUN apt install -y \
        build-essential \
        devscripts \
        quilt \
        git \
        sudo \
        vim \
        procps

    RUN useradd -s /bin/bash -d /home/build -m -U build

    RUN echo "Cmnd_Alias DPKG_ADD_ARCH=/usr/bin/dpkg --add-architecture *" >> /etc/sudoers.d/build
    RUN echo "Cmnd_Alias APT_UPDATE=/usr/bin/apt update -y" >> /etc/sudoers.d/build
    RUN echo "Cmnd_Alias MK_BUILD_DEPS=/usr/bin/mk-build-deps * " >> /etc/sudoers.d/build
    RUN echo "build ALL=(ALL) NOPASSWD:MK_BUILD_DEPS, DPKG_ADD_ARCH, APT_UPDATE" >> /etc/sudoers.d/build

    WORKDIR /home/build
    USER build

    RUN mkdir -p /home/build/packages
