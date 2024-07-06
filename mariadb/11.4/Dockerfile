# -----------------------------------------------------
# MariaDB Image for Pterodactyl
# -----------------------------------------------------
FROM --platform=$TARGETOS/$TARGETARCH mariadb:11.4

LABEL author="Michael Parker" maintainer="parker@pterodactyl.io"

ENV DEBIAN_FRONTEND noninteractive

# Update package list, install netcat, and add 'container' user
RUN apt update -y \
    && apt install -y netcat \
    && useradd -d /home/container -m container -s /bin/bash

# Switch to the 'container' user
USER container

# Set environment variables
ENV USER=container HOME=/home/container

# Set working directory
WORKDIR /home/container

# Copy entrypoint script from the build context to the container
COPY entrypoint.sh /entrypoint.sh

# Specify the command to run when the container starts
CMD ["/bin/bash", "/entrypoint.sh"]
