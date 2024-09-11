FROM ubuntu:22.04
LABEL org.opencontainers.image.source https://github.com/mlwu-ai/devcontainer
LABEL maintainer="Menglin Wu <menglinwoo@163.com>"

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get -qq update && apt-get -qq -y install --no-install-recommends apt-transport-https
RUN apt -qq -y install --reinstall ca-certificates \
  && update-ca-certificates -f \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get -qq -y autoremove \
  && apt-get autoclean \
  && rm -rf /var/lib/apt/lists/* /var/log/dpkg.log

RUN apt-get -qq update && apt-get -qq -y install --no-install-recommends autojump curl ffmpeg fzf git sox sudo tmux wget zsh libsndfile1 \
  libopenmpi-dev openmpi-bin screen zip unzip htop rename \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get -qq -y autoremove \
  && apt-get autoclean \
  && rm -rf /var/lib/apt/lists/* /var/log/dpkg.log



RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && usermod -aG sudo $USERNAME \
  && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER $USERNAME

RUN cd ~ \
  && wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh" \
  && sh Miniforge3-$(uname)-$(uname -m).sh -b \
  && rm Miniforge3-$(uname)-$(uname -m).sh \
  && /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

ENV TERM=xterm-256color
ENV DEBIAN_FRONTEND=dialog
WORKDIR /home/$USERNAME
CMD ["zsh"]
