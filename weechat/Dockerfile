FROM debian:testing-slim

ENV HOME /home/chat
ENV CONFIG_REPO https://github.com/storbeck/configs.git

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
RUN apt-get update -y; apt-get install -q -y \
  git \
  libolm-dev \
  python3 \
  python3-pip \
  dirmngr \
  gpg-agent \
  apt-transport-https \
  weechat-curses \
  weechat-plugins \
  weechat-python \
  weechat-perl \
  rsync \
  vim \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rm -fr /root/.cache

# add chat user
RUN useradd -ms /bin/bash chat && mkdir /var/build

# get and build source code
WORKDIR /var/build
RUN git clone https://github.com/poljar/weechat-matrix.git
WORKDIR /var/build/weechat-matrix
RUN pip3 install -r requirements.txt

# Install and setup autoloading
USER chat
RUN make install
WORKDIR $HOME

# setup matrix bridge
RUN mkdir -p .weechat/python/autoload && \
    ln -s $HOME/.weechat/python/matrix.py $HOME/.weechat/python/autoload/ 

# overlay my configs
RUN git clone $CONFIG_REPO $HOME/configs && \
    rsync -zav $HOME/configs/weechat/* $HOME/.weechat/ && \
    rm -rf $HOME/configs

ENTRYPOINT [ "weechat" ]

