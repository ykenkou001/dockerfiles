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
	openssh-client \
	&& mkdir -p /root/.cache/dein /root/.ssh \
	&& mkdir -p /root/.cache/dein /root/.ssh /home/jovyan/.config/
	# && mkdir -p /root/.cache/dein /root/.ssh
	
# copy id_rsa
COPY ../.ssh/id_rsa /root/.ssh/id_rsa

# WORKDIR /home/jovyan/.config/

# install dein.vim
RUN curl -sf https://raw.githubusercontent.com/Shougo/dein.vim/master/bin/installer.sh \
	| sh -s /root/.cache/dein

# Install vim Plugins
RUN nvim +:UpdateRemotePlugins +qa

# install dein.vim, git clone ykenkou001/nvim
WORKDIR /home/jovyan/.config/

RUN chmod 700 /root/.ssh/ \
	&& ssh-keyscan github.com > /root/.ssh/known_hosts \
	&& git clone git@github.com:ykenkou001/nvim

WORKDIR /work
