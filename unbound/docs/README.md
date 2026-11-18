# Unbound DNS

Validating, recursive DNS resolver ([Unbound](https://nlnetlabs.nl/projects/unbound/about/)) on Ubuntu. Runs as the non-root `unbound` user and logs to stderr.

## Modules Installed
unbound, dns-root-data, ca-certificates, dnsutils

## Usage
```shell
docker run --rm -p 5353:53/udp -p 5353:53/tcp ghcr.io/snigdhasjg/docker-images/unbound
dig @127.0.0.1 -p 5353 example.com
```

## Configuration
Default config is `/etc/unbound/unbound.conf.d/docker.conf` (port 53, loopback and RFC1918 clients, DNSSEC validation, outbound IPv6 off because Docker networks usually lack it; set `do-ip6: yes` if yours has it). Mount your own file over it to customise:
```shell
docker run --rm -v ./my.conf:/etc/unbound/unbound.conf.d/docker.conf:ro ...
```
