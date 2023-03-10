# jupyter notebookが使えるpython環境
FROM jupyter/minimal-notebook

USER root

RUN apt-get update \
	# && apt-get upgrade -y \
	&& apt-get remove -y --purge vim-tiny \
	&& apt-get install -y \
	--no-install-recommends \
	# install neovim
	neovim \
	tmux \
	curl \
	git \
	gcc \
	libxml2-dev \
    libxslt-dev \
    # linux-headers \
    musl-dev \
	python3-pip \
	openssh-client \
	&& apt-get autoremove -y \
	&& apt-get clean -y \
	# && mkdir -p /root/.cache/dein /root/.ssh \
	&& mkdir -p /home/jovyan/.cache/dein /root/.ssh /home/jovyan/.config/
	
# copy id_rsa
COPY ../.ssh/id_rsa /root/.ssh/id_rsa

# git clone ykenkou001/nvim
WORKDIR /home/jovyan/.config/

RUN chmod 700 /root/.ssh/ \
	&& ssh-keyscan github.com > /root/.ssh/known_hosts \
	&& git clone git@github.com:ykenkou001/nvim

WORKDIR /work
