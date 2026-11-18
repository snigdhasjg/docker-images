ARG UBUNTU_VERSION=26.04
FROM ubuntu:${UBUNTU_VERSION}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        ca-certificates unbound dns-root-data dnsutils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /etc/unbound/unbound.conf.d/remote-control.conf /etc/unbound/unbound.conf.d/root-auto-trust-anchor-file.conf

# Drop-in config: listen on all interfaces, log to stderr, allow private ranges
COPY unbound.conf /etc/unbound/unbound.conf.d/docker.conf

# The unbound package already creates the non-root `unbound` user and group
USER unbound

EXPOSE 53/udp 53/tcp

CMD ["unbound", "-d", "-c", "/etc/unbound/unbound.conf"]
