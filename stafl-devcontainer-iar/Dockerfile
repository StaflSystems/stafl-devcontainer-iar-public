ARG BXARM=non-fs

FROM ghcr.io/staflsystems/stafl-devcontainer-ci:0.3.2-0 AS stafl-devcontainer-iar-non-fs
COPY iar/bxarm-*.deb /tmp
ENV PATH "$PATH:/opt/iarsystems/bxarm/arm/bin"

FROM ghcr.io/staflsystems/stafl-devcontainer-ci:0.3.2-0 AS stafl-devcontainer-iar-fs
COPY iar/bxarmfs-*.deb /tmp
ENV PATH "$PATH:/opt/iarsystems/bxarmfs/arm/bin"

FROM stafl-devcontainer-iar-${BXARM}

COPY user-setup-scripts/ /user-setup-scripts/

RUN  export DEBIAN_FRONTEND=noninteractive && \
     apt-get update && \
     apt-get install --no-install-recommends -y sudo libsqlite3-0 libxml2 tzdata && \
     apt-get install --no-install-recommends -y /tmp/bx*.deb && \
     apt-get clean autoclean autoremove && \
     rm -rf /tmp/*.deb

WORKDIR ${HOME}