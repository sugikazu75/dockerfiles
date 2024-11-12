FROM ubuntu:22.04

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y

RUN apt-get install -y git emacs

RUN apt-get install -y vim less ca-certificates sudo bash-completion python3-pip tmux python-is-python3 && \
    pip3 install catkin-tools && \
    echo "deb [trusted=yes] https://raw.githubusercontent.com/sugikazu75/ros-o-builder/jammy-one-unstable/repository ./" | sudo tee /etc/apt/sources.list.d/sugikazu75_ros-o-builder.list && \
    apt-get update && \
    apt-get install -y python3-rosdep2 && \
    echo "yaml https://raw.githubusercontent.com/sugikazu75/ros-o-builder/jammy-one-unstable/repository/local.yaml debian" | sudo tee /etc/ros/rosdep/sources.list.d/1-sugikazu75_ros-o-builder.list && \
    rosdep update && \
    apt-get install -y ros-one-desktop-full && \
    apt-get install -y python3-wstool

RUN source /opt/ros/one/setup.bash && \
    mkdir -p ~/ros/jsk_aerial_robot_ws/src && cd ~/ros/jsk_aerial_robot_ws && \
    wstool init src && \
    wstool set -u -y -t src jsk_aerial_robot http://github.com/jsk-ros-pkg/jsk_aerial_robot --git && \
    wstool merge -t src src/jsk_aerial_robot/aerial_robot_${ROS_DISTRO}.rosinstall && \
    wstool update -t src && \
    rosdep install -y -r --from-paths src --ignore-src --rosdistro $ROS_DISTRO && \
    catkin build --no-status
