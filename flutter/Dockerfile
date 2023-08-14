FROM nginx:latest

RUN apt update && apt install -y curl git unzip xz-utils zip file libglu1-mesa wget vim neovim clang cmake ninja-build pkg-config libgtk-3-dev

RUN mkdir /home/flutterdev
WORKDIR /home/flutterdev

# Download Flutter SDK
COPY google-chrome-stable_current_amd64.deb /home/flutterdev
COPY flutter_linux_3.10.6-stable.tar.xz /home/flutterdev
RUN tar xf ./flutter_linux_3.10.6-stable.tar.xz; \
    git config --global --add safe.directory /home/flutterdev/flutter; \
    apt-get install -y ./google-chrome-stable_current_amd64.deb; \
    rm -rf google-chrome-stable_current_amd64.deb flutter_linux_3.10.6-stable.tar.xz

ENV PATH "$PATH:/home/flutterdev/flutter/bin:$HOME/.pub-cache/bin"

# Precache flutter libraries & run basic checks
RUN flutter precache; \
    flutter doctor; \
    dart pub global activate stacked_cli

COPY nginx.conf /etc/nginx/

EXPOSE 8080
STOPSIGNAL SIGQUIT

CMD ["nginx", "-g", "daemon off;"]

