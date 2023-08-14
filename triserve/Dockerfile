FROM node:current

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
                vim \
                git \
		ssh \
	; \
	rm -rf /var/lib/apt/lists/*

# Copy a .vimrc file into the container with basic settings
COPY ./node_vimrc /root/.vimrc

RUN set -eux; \
# Install Vue Vim plugin
        curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim; \
        /usr/bin/vim +'PlugInstall' +qa -i NONE; \
# Install some node packages
        npm install -g npm@9.6.2; \
	npm install -g http-server 

EXPOSE 55000
CMD ["http-server", "dist"]
