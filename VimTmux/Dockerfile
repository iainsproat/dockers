FROM ubuntu:latest

ARG goversion=1.10

ENV GOPATH="${HOME}/workspace"
ENV GOROOT="/usr/lib/go-${goversion}"
ENV PATH="$PATH:${GOROOT}/bin"

RUN DEBIAN_FRONTEND=noninteractive                                && \
    apt-get update                                                && \
    apt-get install  -y --no-install-recommends \
        software-properties-common
RUN DEBIAN_FRONTEND=noninteractive                                && \
    add-apt-repository ppa:neovim-ppa/stable -y                   && \
    add-apt-repository ppa:gophers/archive -y                     && \
    apt-get update                                                && \
    apt-get upgrade -y                                            && \
    apt-get install -y --no-install-recommends \
        apt-utils \
        build-essential \
        ca-certificates \
        curl \
        git \
        libssl-dev \
        tmux \
        neovim \
        python3-dev \
        python3-pip \
        nodejs \
        npm  \
        golang-${goversion}-go                                     && \
    rm -rf \
        /usr/lib/go \
        /var/cache/* \
        /var/log/* \
        /var/tmp/*

RUN pip3 install --upgrade pip                                     && \
    pip3 install setuptools                                        && \
    git clone https://github.com/luan/vimfiles.git "${HOME}"/.vim  && \
    cd "${HOME}"/.vim                                              && \
    git checkout master                                            && \
    git pull -r                                                    && \
    ./update

ADD ./tmux.conf /root/.tmux.conf
RUN mkdir -p "${HOME}"/.tmux/plugins && \
    git clone https://github.com/tmux-plugins/tpm "${HOME}"/.tmux/plugins/tpm

ENV SHELL="/bin/bash"
ENV TERM=xterm-256color

CMD ["bash", "-l"]