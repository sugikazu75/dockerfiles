FROM ubuntu:22.04

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y

RUN apt-get install -y curl sudo lsb-release

RUN curl -sSL https://ros.packages.techfak.net/gpg.key -o /etc/apt/keyrings/ros-one-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/ros-one-keyring.gpg] https://ros.packages.techfak.net $(lsb_release -cs)-testing main" | sudo tee /etc/apt/sources.list.d/ros1.list && \
    echo "# deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/ros-one-keyring.gpg] https://ros.packages.techfak.net $(lsb_release -cs)-testing main-dbg" | sudo tee -a /etc/apt/sources.list.d/ros1.list

RUN apt-get update -y && \
    apt-get install python3-rosdep -y

RUN rosdep init
    
RUN echo "yaml https://ros.packages.techfak.net/ros-one.yaml one" | sudo tee /etc/ros/rosdep/sources.list.d/1-ros-one.list && \
    rosdep update

RUN apt-get install ros-one-desktop -y
