FROM fedora:27
MAINTAINER Hajime Tazaki <thehajime@gmail.com>

RUN dnf install -y 'dnf-command(debuginfo-install)'
RUN dnf update -y
RUN dnf install -y mercurial expat-devel git-core gcc gcc-c++ bison flex openssl-devel \
       libdb-devel libpcap-devel libsysfs-devel gawk indent pkgconfig autoconf automake sudo \
       bzip2 ccache saxon
RUN dnf debuginfo-install -y glibc

RUN adduser ns3dce && \
    echo "ns3dce ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/ns3dce && \
    chmod 0440 /etc/sudoers.d/ns3dce

RUN echo "#!/bin/sh" > /usr/bin/saxonb-xslt && \
    echo 'exec java -classpath /usr/share/java/saxonb.jar net.sf.saxon.Transform "$@"' > /usr/bin/saxonb-xslt && \
    chmod 755 /usr/bin/saxonb-xslt

USER ns3dce
WORKDIR /home/ns3dce/

ENV PATH /usr/lib64/ccache:${PATH}
