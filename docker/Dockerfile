FROM ubuntu:latest

# System environment variable
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

# Environment variable for this container
ENV FLUTTER_DIR=/opt/flutter
ENV WORK_DIR=/root
ENV GITHUB_REPO=flutter-dev-container
ENV GITHUB_USER=tuimac
ENV GITHUB_EMAIL=tuimac.devadm01@gmail.com
ENV PJT_DIR="${WORK_DIR}/${GITHUB_REPO}/app"
ENV ANDROID_DIR=/opt/android
ENV ANDROID_HOME=${ANDROID_DIR}/cmdline-tools
ENV ANDROID_SDK_ROOT=${ANDROID_HOME}
ENV PORT=80
ENV PATH="${PATH}:${FLUTTER_DIR}/bin:${ANDROID_HOME}/bin"
ENV ANDROID_SDK_VERSION=9477386

EXPOSE ${PORT}

WORKDIR ${WORK_DIR}

SHELL ["/bin/bash", "-c"]

RUN apt update && \
    apt upgrade -y && \
    apt install -y git unzip tree curl jq clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev default-jdk fonts-liberation libu2f-udev libvulkan1 wget xdg-utils && \
    apt --fix-broken install && \
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    dpkg -i google-chrome-stable_current_amd64.deb && \
    rm -rf google-chrome-stable_current_amd64.deb && \
    git config --global user.email ${GITHUB_EMAIL} && \
    git config --global user.user ${GITHUB_USER} && \
    curl https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_VERSION}_latest.zip -o cmdline-tools.zip && \
    unzip cmdline-tools.zip -d ${ANDROID_DIR} && \
    git clone https://github.com/flutter/flutter.git -b stable --depth 1 ${FLUTTER_DIR} && \
    flutter channel stable && \
    flutter upgrade && \
    flutter doctor && \
    flutter config --enable-web && \
    flutter precache && \
    git clone https://github.com/${GITHUB_USER}/${GITHUB_REPO}.git && \
    cd ${PJT_DIR} && \
    flutter pub get
