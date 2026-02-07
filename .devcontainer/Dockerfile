# For details, see https://github.com/devcontainers/images/tree/main/src/ruby
FROM mcr.microsoft.com/devcontainers/ruby:1-3.3-bookworm

# Install node version from .nvmrc
WORKDIR /app
COPY .nvmrc .
RUN /bin/bash --login -i -c "nvm install"

# install Yarn
# ref: https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /etc/apt/keyrings/yarn-archive-keyring.gpg && \
    echo "deb [signed-by=/etc/apt/keyrings/yarn-archive-keyring.gpg] https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

# Install additional OS packages
RUN apt-get update && \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get -y install --no-install-recommends libicu-dev libidn11-dev ffmpeg libvips42 libpam-dev

# Disable download prompt for Corepack
ENV COREPACK_ENABLE_DOWNLOAD_PROMPT=0

# Move welcome message to where VS Code expects it
COPY .devcontainer/welcome-message.txt /usr/local/etc/vscode-dev-containers/first-run-notice.txt
