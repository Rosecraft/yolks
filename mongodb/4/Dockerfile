# ----------------------------------
# Environment: MongoDB
# ----------------------------------

# Use the official MongoDB image with platform specific tag (if needed)
FROM --platform=$TARGETOS/$TARGETARCH mongo:4-focal

# Label the image with author and maintainer information
LABEL author="Michael Parker" maintainer="parker@pterodactyl.io"

# Set environment variable for non-interactive package installation
ENV DEBIAN_FRONTEND noninteractive

# Download pre-built MongoDB binaries (alternative to using apt)
RUN curl -L https://repo.mongodb.org/apt/archive/apt/v4.4/mongodb-org/stable/mongodb-org_${MONGODB_VERSION:-4.4.2}-1~focal_${TARGETARCH}.deb -o /tmp/mongodb.deb

# Create a directory for MongoDB binaries
RUN mkdir -p /usr/local/mongodb

# Copy the downloaded binary to the installation directory
COPY --from=0 /tmp/mongodb.deb /usr/local/mongodb/mongodb.deb

# Unpack the binary
RUN dpkg -i /usr/local/mongodb/mongodb.deb

# Set the path to the MongoDB binary (optional, depending on entrypoint.sh)
ENV PATH=/usr/local/mongodb/bin:$PATH

# Switch user to the container user
USER container

# Set environment variables for user and home directory
ENV USER=container HOME=/home/container

# Set working directory
WORKDIR /home/container

# Copy the entrypoint script
COPY ./entrypoint.sh /entrypoint.sh

# Run the entrypoint script as the container user
CMD ["/bin/bash", "-c", "source /entrypoint.sh && "$@""]
