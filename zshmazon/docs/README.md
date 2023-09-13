Welcome to ZSHmazon – Your Ultimate AmazonLinux Image with Zsh Magic!

Discover a world of command-line sophistication with our ZSHmazon Docker image. We've curated the perfect AmazonLinux environment enhanced with the power of Zsh, Oh-My-Zsh. Elevate your terminal experience with this feature-packed image, designed to boost your productivity and style.

Whether you're a developer, system administrator, or terminal enthusiast, ZSHmazon empowers you with a captivating, efficient, and fun command-line experience. Download now and unlock the full potential of your AmazonLinux-based containers.

<img src="https://raw.githubusercontent.com/snigdhasjg/docker-images/main/zshmazon/docs/terminal.png" width="512" alt="Terminal Example">

## Key Features:

- AmazonLinux base with [Zsh](https://en.wikipedia.org/wiki/Z_shell) magic.
- [Oh-My-Zsh](https://ohmyz.sh) for enhanced shell capabilities.
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k) for eye-catching, customizable prompts.
- [Syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) for code clarity.
- Vibrant [auto-suggestions](https://github.com/zsh-users/zsh-autosuggestions) for faster typing.
- [Zsh Docker Aliases](https://github.com/akarzim/zsh-docker-aliases) for streamlined container management.

## Modules Installed
zsh, sudo, vim, tar, iputils, git, tig

## How to Use ZSHmazon

### Run the ZSHmazon Docker Sandbox:
- To run the Docker image with the previously created volume mounted to `/home/sandbox` for the user `sandbox`, use the following command:
```shell
docker run --name sandbox -v zshmazon-sandbox:/home/sandbox --rm -it macabrequinox/zshmazon
```
- Along with running the container, this command creates a docker volume named `zshmazon-sandbox`.
- This command starts the ZSHmazon Docker container, providing you with a secure and permission-free environment to run commands and experiment.
- Once you exit, it automatically deletes the container instance.

Now you're ready to enjoy your ZSHmazon Docker Sandbox, where you can safely execute commands without worrying about permissions or security issues. 
Feel free to customize your environment and configurations within the sandbox, and any changes on home directory will be stored in the `zshmazon-sandbox` volume for future use.

### To Have a Fresh Start Again:
- reset all settings just delete the `ZSHmazon-sandbox` volume by running the following command:
```shell
docker volume rm zshmazon-sandbox
```
- This volume was storing your configuration and setups of docker image's home directory.

## Contribute
On [GitHub](https://github.com/snigdhasjg/docker-images/tree/main/zshmazon) by editing the [Dockerfile](https://github.com/snigdhasjg/docker-images/tree/main/zshmazon/Dockerfile)

[![Docker Hub Description](https://github.com/snigdhasjg/docker-images/actions/workflows/docker-hub-description.yml/badge.svg)](https://github.com/snigdhasjg/docker-images/actions/workflows/docker-hub-description.yml)
[![Docker Image Build](https://github.com/snigdhasjg/docker-images/actions/workflows/docker-image-build.yml/badge.svg)](https://github.com/snigdhasjg/docker-images/actions/workflows/docker-image-build.yml)

---
Tags: #AmazonLinux #Zsh #OhMyZsh #Powerlevel10k #SyntaxHighlighting #AutoSuggestions #DockerImage #CommandLine #DeveloperTools #Productivity