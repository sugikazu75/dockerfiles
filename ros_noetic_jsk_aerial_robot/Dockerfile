FROM ubuntu:20.04

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y

RUN apt-get install -y git emacs

RUN apt-get install -y wget sudo lsb-release gnupg sed build-essential

RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' && \
    apt-get install -y curl && \
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add - && \
    apt-get update -y && \
    apt-get install -y ros-noetic-desktop-full && \
    apt-get install -y python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential python3-catkin-tools

RUN rosdep init && \
    rosdep update

RUN source /opt/ros/noetic/setup.bash && \
    mkdir -p ~/ros/jsk_aerial_robot_ws/src && \
    cd ~/ros/jsk_aerial_robot_ws && \
    wstool init src && \
    wstool set -u -y -t src jsk_aerial_robot http://github.com/jsk-ros-pkg/jsk_aerial_robot --git && \
    wstool merge -t src src/jsk_aerial_robot/aerial_robot_${ROS_DISTRO}.rosinstall && \
    wstool update -t src && \
    rosdep install -y -r --from-paths src --ignore-src --rosdistro $ROS_DISTRO && \
    catkin build --no-status
