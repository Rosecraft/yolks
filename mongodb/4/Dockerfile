# ----------------------------------
# Environment: MongoDB
# ----------------------------------
FROM        --platform=$TARGETOS/$TARGETARCH mongo:4-focal

LABEL       author="Michael Parker" maintainer="parker@pterodactyl.io"

ENV         DEBIAN_FRONTEND noninteractive

RUN gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 656408E390CFB1F5 \
    || gpg --keyserver keyserver.ubuntu.com --recv-keys 656408E390CFB1F5 \
    || gpg --keyserver pgp.mit.edu --recv-keys 656408E390CFB1F5

RUN curl -fsSL https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x656408E390CFB1F5 | apt-key add -


RUN         apt update -y \
            && apt install -y netcat-openbsd iproute2 \
            && useradd -d /home/container -m container -s /bin/bash

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
