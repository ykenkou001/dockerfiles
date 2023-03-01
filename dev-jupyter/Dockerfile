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
	&& mkdir -p /root/.cache/dein /root/.ssh /root/.config/nvim
	
# copy id_rsa
COPY ../.ssh/id_rsa /root/.ssh/id_rsa

WORKDIR /root/.config/nvim

# install dein.vim 
# git clone nvim-r-docker/nvim
RUN chmod 700 /root/.ssh/ \
	&& ssh-keyscan github.com > /root/.ssh/known_hosts \
	&& git clone git@github.com:ykenkou001/nvim-r-docker.git

WORKDIR /code
