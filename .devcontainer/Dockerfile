ARG VARIANT=2.7-bullseye
FROM mcr.microsoft.com/vscode/devcontainers/ruby:${VARIANT}

WORKDIR /home/

# ENV Variables required by Jekyll
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    TZ=Etc/UTC \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US

RUN gem install bundler github-pages

COPY . .

ENV DEBIAN_FRONTEND=noninteractive
RUN sh ./setup.sh

RUN echo 'export NVM_DIR="$HOME/.nvm"' >> "$HOME/.zshrc"
RUN echo '\n' >> "$HOME/.zshrc"