FROM ubuntu:22.04

ARG USER=autoware
ARG UID=1000
ARG GID=$UID

ENV HOME /home/$USER
ENV PATH=/home/$USER/.local/bin:$PATH

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install \
      sudo \
      git \
      python3 \
      python3-pip \
      python-is-python3 \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN groupadd work -g $GID \
    && useradd -ms /bin/bash $USER -g $GID -u $UID \
    && printf "$USER:$USER" | chpasswd \
    && printf "$USER ALL= NOPASSWD: ALL\\n" >> /etc/sudoers

USER $USER
WORKDIR $HOME

RUN python -m pip install --user --no-cache-dir pre-commit
