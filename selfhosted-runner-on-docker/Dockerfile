FROM ubuntu:22.04

# Install basic utilities
RUN apt-get update && apt-get install -y init systemd \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    sudo \
    systemd \
    && rm -rf /var/lib/apt/lists/*


# Install Docker の GPG キーとリポジトリを追加
RUN install -m 0755 -d /etc/apt/keyrings \
    && curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc \
    && chmod a+r /etc/apt/keyrings/docker.asc



RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    | tee /etc/apt/sources.list.d/docker.list > /dev/null


# Docker をインストール
RUN apt-get update && apt-get install -y \
    docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin \
    && rm -rf /var/lib/apt/lists/*


# actions-runner ユーザーを作成
RUN useradd -m actions-runner -s /bin/bash && \
    echo "actions-runner:actions-runner" | chpasswd && \
    usermod -aG docker,sudo actions-runner



