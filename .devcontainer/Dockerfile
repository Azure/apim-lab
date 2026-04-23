ARG VARIANT=3.2-bookworm
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

# Convert line endings from CRLF to LF (in case files were edited on Windows)
RUN sed -i 's/\r$//' ./setup.sh

ENV DEBIAN_FRONTEND=noninteractive
RUN bash ./setup.sh

RUN echo 'export NVM_DIR="$HOME/.nvm"' >> "$HOME/.zshrc"
RUN echo '\n' >> "$HOME/.zshrc"