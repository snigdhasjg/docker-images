Welcome to GitHub CLI

This Docker image provides a lightweight environment to run the GitHub CLI (`gh`) on a Debian-based system. It’s perfect for integrating GitHub commands into your CI/CD pipelines or any automated workflows.

## Features

- **Base Image**: Built on `debian:trixie-slim` for a minimal footprint.
- **Installed Tools**: 
  - `curl`
  - `git`
  - `jq`
  - `ca-certificates`
- **GitHub CLI**: The latest version of GitHub CLI installed.

## Getting Started

### Prerequisites

Make sure you have Docker installed on your machine. You can download it from [Docker's official website](https://www.docker.com/get-started).

### Build the Image

To build the Docker image, navigate to the directory containing the `Dockerfile` and run:

```bash
docker build -t github-cli .
```

### Run the Container

To run the GitHub CLI in a new container, use:

```bash
docker run --rm -it github-cli
```

You can pass any `gh` command as an argument. For example:

```bash
docker run --rm -it github-cli auth login
```

## Usage

Once inside the container, you can use the `gh` commands just like you would on your local machine. For example:

```bash
gh repo list
```

## Contributing

If you want to contribute to this project, feel free to fork the repository and submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Thanks to the [GitHub CLI team](https://github.com/cli/cli) for their excellent work on the tool.
- Inspired by the Debian community for providing a robust base image.

Enjoy using the GitHub CLI in your Dockerized environments!