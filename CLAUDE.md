# CLAUDE.md

Collection of Docker images, one folder per image. Each image is built and published to GHCR by a single workflow.

## Layout

```
<image>/
  Dockerfile              # required: its presence is what makes the folder an image
  .dockerignore           # keeps docs/ and *.md out of the build context
  docs/
    README.md             # image documentation (shown on the package page / repo)
    short_description.txt # one line; becomes the org.opencontainers.image.description label
.github/workflows/build.yml
```

Currently only `zshbuntu/` exists (Ubuntu + zsh, Oh-My-Zsh, powerlevel10k, plugins, passwordless-sudo `sandbox` user, uid 1001).

## Adding an image

Create `<name>/Dockerfile` (plus `docs/short_description.txt`, `docs/README.md`, `.dockerignore`). No workflow edits are needed: `build.yml` discovers every folder containing a `Dockerfile` and builds each in a matrix. The folder name becomes the image name.

## CI (`.github/workflows/build.yml`)

- Jobs: `prepare-folders` (find Dockerfiles, emit JSON matrix) -> `version` (paulhatch/semantic-version, tag prefix `v`, bump on every commit) -> `build` (matrix, `linux/amd64,linux/arm64`, QEMU + Buildx) -> `tag` (push only, creates the git tag once every image built).
- Pushes to `main` publish `ghcr.io/<owner>/<repo>/<image>:<version>` and `:latest` (lowercased). PRs build only; they never log in or push.
- Version bumps come from commit messages: `!:`, `BREAKING CHANGE:`, `MAJOR:` -> major; `FEAT:`, `FEATURE:`, `MINOR:` -> minor; anything else -> patch.
- Pushes touching only `**/docs/**` or `**.md` do not trigger a build.
- Auth is `GITHUB_TOKEN` only (no Docker Hub, no repo secrets). Package visibility is set on GitHub after the first push (new packages start private).
- Action versions are deliberately current (checkout v7, buildx/login v4, build-push v7, github-script v9); keep new steps consistent.

## Dockerfile conventions (see `zshbuntu/Dockerfile`)

- Base version is an `ARG` at the top (`UBUNTU_VERSION`), set to the latest LTS.
- Single `apt-get` layer: `update`, `install -y --no-install-recommends`, `clean`, remove `/var/lib/apt/lists/*`; `DEBIAN_FRONTEND=noninteractive`.
- Non-root user `sandbox` with its own group (not in `root`). Do not re-add `-g root`.
- `systemd`, the unpinned `git clone --depth=1` plugins, the oh-my-zsh installer from `master`, and powerlevel10k are intentional; do not pin or remove them.
- The `.zshrc` `sed` edits are followed by a `grep -q` so the build fails if the oh-my-zsh template changes.
- No `HEALTHCHECK` by design.

## Verify locally

```sh
docker build -t zshbuntu-test zshbuntu/
docker run --rm zshbuntu-test zsh -c 'id; grep ^plugins ~/.zshrc'
```

Workflows cannot be run locally; validate YAML with `python3 -c "import yaml,sys; yaml.safe_load(open(sys.argv[1]))" .github/workflows/build.yml`.

## License

MPL-2.0 (`LICENSE`, and the `org.opencontainers.image.licenses` label in `build.yml`).
