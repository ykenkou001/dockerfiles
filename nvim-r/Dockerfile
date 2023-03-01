# FROM r-base/tidyverse:latest
# FROM rocker/rstudio:latest
FROM rocker/tidyverse:latest
RUN apt-get update \
	# && apt-get upgrade -y \
	&& apt-get remove -y --purge vim-tiny \
	&& apt-get install -y \
	--no-install-recommends \
	# For languageserver --------------------
	build-essential \
	libcurl4-openssl-dev \
	libssl-dev \
	# For languageserver --------------------
	neovim \
	tmux \
	curl \
	git \
	gcc \
	python3-pip \
	# x window System
	# xorg \
	# 日本語フォントをインストールする \
	# fonts-ipaexfont \
	# fonts-noto-cjk \
	&& apt-get autoremove -y \
	&& apt-get clean -y \
	&& mkdir -p /root/.cache/dein \
	# Install R packages
	&& R -e "install.packages('languageserver', dependencies=TRUE)" \
	&& R -e "install.packages('httpgd', dependencies=TRUE)"

# Install httpgd and dependent packages.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    libfontconfig1-dev \
    && apt-get autoremove -y \
	&& apt-get clean -y \
	&& rm -rf /var/lib/apt/lists/* \
    && install2.r --error --skipinstalled --ncpu -1 \
    httpgd \
    && rm -rf /tmp/downloaded_packages

# install dein.vim
RUN curl -sf https://raw.githubusercontent.com/Shougo/dein.vim/master/bin/installer.sh \
	| sh -s /root/.cache/dein

# Install vim Plugins
RUN nvim +:UpdateRemotePlugins +qa

RUN pip install pynvim

# Set default values used in the httpgd::hgd() function.
RUN echo 'options(httpgd.host = "0.0.0.0", httpgd.port = 8888)' >> /etc/R/Rprofile.site

EXPOSE 8888

COPY /nvim/ /root/.config/nvim

WORKDIR /code/

COPY /pjt ./pjt/
COPY /work ./work/
COPY .Rprofile .

# RUN chmod -R 777 /root
# ENTRYPOINT ["nvim"]
