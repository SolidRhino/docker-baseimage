FROM arm32v6/alpine:latest
LABEL maintainer="Solid Rhino"

# qemu arm static binary
COPY tmp/qemu-arm-static /usr/bin/qemu-arm-static

# root filesystem
COPY rootfs /

# base image packages
RUN apk -U update && \
    apk -U upgrade && \
    apk -U add --no-cache \
        bash \
        coreutils \
        ca-certificates \
        shadow \
        curl

# s6 overlay
RUN curl -L https://github.com/just-containers/s6-overlay/releases/download/v1.22.1.0/s6-overlay-armhf.tar.gz \
    | tar -xzC /

# create default user / group and folders
RUN groupadd -g 1000 abc && \
    useradd -u 1000 -g abc -d /app -s /bin/false abc && \
    mkdir -p \
	    /app \
	    /config

ENTRYPOINT ["/init"]