FROM ubuntu:17.04
MAINTAINER Hajime Tazaki <thehajime@gmail.com>

RUN apt-get update
RUN apt-get install -y mercurial libexpat1-dev git-core build-essential bison \
    flex libssl-dev libdb-dev libpcap-dev libc6-dbg libsysfs-dev gawk indent \
    pkg-config autoconf automake sudo ccache libsaxonb-java openjdk-8-jre-headless && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash ns3dce && adduser ns3dce sudo && echo -n 'ns3dce:ns3dce' | chpasswd

# Enable passwordless sudo for users under the "sudo" group
RUN sed -i.bkp -e \
      's/%sudo\s\+ALL=(ALL\(:ALL\)\?)\s\+ALL/%sudo ALL=NOPASSWD:ALL/g' \
      /etc/sudoers

USER ns3dce
WORKDIR /home/ns3dce/

ENV PATH /usr/lib/ccache:${PATH}
