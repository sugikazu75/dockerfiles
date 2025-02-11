FROM ubuntu:20.04

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y

RUN apt-get install -y build-essential lsb-release sudo texlive texlive-lang-cjk texlive-lang-japanese texlive-science texlive-fonts-recommended texlive-fonts-extra jbibtex-base nkf
