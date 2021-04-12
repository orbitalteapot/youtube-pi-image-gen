ARG BASE_IMAGE=i386/debian:buster

FROM ${BASE_IMAGE}

WORKDIR /build
ARG DEBIAN_FRONTEND=noninteractive
ENV DEBIAN_FRONTEND=${DEBIAN_FRONTEND}

RUN apt-get -y update && \
    apt-get -y install --no-install-recommends \
    git vim parted \
    quilt coreutils qemu-user-static debootstrap zerofree zip dosfstools \
    libarchive-tools libcap2-bin rsync grep udev xz-utils curl xxd file kmod bc\
    binfmt-support ca-certificates schroot git qemu-utils kpartx\
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/RPi-Distro/pi-gen.git
WORKDIR /build/pi-gen/
COPY config/ .
RUN find . -name '*.sh' | xargs chmod +x
RUN dpkg-reconfigure qemu-user-static
