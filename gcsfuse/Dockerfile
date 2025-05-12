# Use the Google Cloud SDK Debian-based image as the base image
FROM gcr.io/google.com/cloudsdktool/cloud-sdk:slim

# Install required dependencies and gcsfuse
RUN export GCSFUSE_REPO=gcsfuse-$(lsb_release -c -s) && \
    echo "deb https://packages.cloud.google.com/apt $GCSFUSE_REPO main" | tee /etc/apt/sources.list.d/gcsfuse.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update && \
    apt-get install -y fuse gcsfuse && \
    apt-get clean

# Optionally: Verify installation
ENTRYPOINT ["gcsfuse"]