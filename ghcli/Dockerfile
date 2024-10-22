FROM debian:trixie-slim

RUN apt update && \
    apt-get install ca-certificates wget curl git jq -y --no-install-recommends && \
	mkdir -p -m 755 /etc/apt/keyrings && \
	wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null && \
	chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg && \
	echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null && \
	apt update && \
	apt install gh -y --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT [ "gh" ]