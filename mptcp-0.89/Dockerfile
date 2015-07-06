FROM ubuntu:12.04
MAINTAINER Hajime Tazaki <thehajime@gmail.com>

RUN apt-get update
RUN apt-get install -y mercurial libexpat1-dev git-core build-essential bison flex libssl-dev libdb-dev libpcap-dev libc6-dbg pkg-config libncurses-dev

ADD add-defconfig /
WORKDIR /var/lib/mptcp-0.89
RUN mkdir -p /var/lib/mptcp-0.89

RUN git clone git://github.com/multipath-tcp/mptcp -b mptcp_v0.89
WORKDIR /var/lib/mptcp-0.89/mptcp
RUN git remote add dce git://github.com/direct-code-execution/net-next-sim.git
RUN git fetch dce
RUN git merge dce/sim-ns3-3.11.0-branch
RUN cat /add-defconfig >> arch/sim/defconfig

RUN make clean ARCH=sim
RUN make defconfig ARCH=sim
RUN make library ARCH=sim OPT=no

WORKDIR /var/lib/mptcp-0.89/mptcp/arch/sim/test
RUN make testbin
WORKDIR /var/lib/mptcp-0.89/mptcp/
RUN make test ARCH=sim ADD_PARAM="-r"
