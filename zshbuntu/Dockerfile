ARG UBUNTU_VERSION=26.04
FROM ubuntu:${UBUNTU_VERSION}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        ca-certificates zsh sudo systemd vim git tig \
        curl iputils-ping net-tools iproute2 dnsutils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Creating user
RUN useradd -rm -d /home/sandbox -s /usr/bin/zsh -u 1001 sandbox && \
    echo "sandbox ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/sudoers

USER sandbox
WORKDIR /home/sandbox

RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
RUN git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions && \
    git clone --depth=1 https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting && \
    git clone --depth=1 https://github.com/akarzim/zsh-docker-aliases.git  ~/.oh-my-zsh/custom/plugins/zsh-docker-aliases && \
    sed -i -E 's/^plugins=\(.*\)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting zsh-docker-aliases)/' .zshrc && \
    grep -q '^plugins=(git zsh-autosuggestions' .zshrc && \
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k && \
    sed -i 's|ZSH_THEME=.*|ZSH_THEME="powerlevel10k/powerlevel10k"|' .zshrc

RUN git config --global init.defaultBranch main && \
    git config --global user.name "Ubuntu Sandbox" && \
    git config --global user.email "sandbox@ubuntu.sandbox"

CMD ["zsh"]