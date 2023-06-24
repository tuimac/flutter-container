FROM ubuntu:latest

ENV FLUTTER_DIR=/opt/flutter
ENV WORK_DIR=/root
ENV GITHUB_REPO=flutter-dev-container
ENV GITHUB_USER=tuimac
ENV PJT_DIR="${WORK_DIR}/${GITHUB_REPO}"
ENV PORT=80
ENV PATH="${PATH}:${FLUTTER_DIR}/bin"

EXPOSE ${PORT}

WORKDIR ${WORK_DIR}

SHELL ["/bin/bash", "-c"]

RUN apt update && \
    apt upgrade -y && \
    apt install -y git unzip tree curl jq clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev default-jdk fonts-liberation libu2f-udev libvulkan1 wget xdg-utils android-sdk && \
    apt --fix-broken install && \
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    dpkg -i google-chrome-stable_current_amd64.deb && \
    rm -rf google-chrome-stable_current_amd64.deb && \
    echo "Asia/Tokyo" > /etc/timezone && \
    git clone https://github.com/flutter/flutter.git -b stable --depth 1 ${FLUTTER_DIR} && \
    flutter channel stable && \
    flutter upgrade && \
    flutter doctor && \
    flutter config --enable-web && \
    flutter precache && \
    git clone https://github.com/${GITHUB_USER}/${GITHUB_REPO}.git
