FROM ubuntu:22.04

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y

RUN apt-get install -y git

RUN apt-get install -y vim less ca-certificates sudo bash-completion python3-pip git tmux python-is-python3 && \
    pip3 install catkin-tools && \
    echo "deb [trusted=yes] https://raw.githubusercontent.com/v4hn/ros-o-builder/jammy-one-unstable/repository ./" | sudo tee /etc/apt/sources.list.d/v4hn_ros-o-builder.list && \
    apt-get update && \
    apt-get install -y python3-rosdep2 && \
    echo "yaml https://raw.githubusercontent.com/v4hn/ros-o-builder/jammy-one-unstable/repository/local.yaml debian" | sudo tee /etc/ros/rosdep/sources.list.d/1-v4hn_ros-o-builder.list && \
    rosdep update && \
    apt-get install -y ros-one-desktop-full && \
    apt-get install -y python3-wstool

RUN source /opt/ros/one/setup.bash && \
    mkdir -p ~/ros/jsk_aerial_robot_ws/src && cd ~/ros/jsk_aerial_robot_ws && \
    wstool init src && \
    cd ~/ros/jsk_aerial_robot_ws/src && git clone -b GA/jammy https://github.com/sugikazu75/jsk_aerial_robot.git && \
    cd ~/ros/jsk_aerial_robot_ws && wstool merge -t src src/jsk_aerial_robot/aerial_robot_${ROS_DISTRO}.rosinstall && \
    wstool update -t src && \
    rosdep install -y -r --from-paths src --ignore-src --rosdistro $ROS_DISTRO || true && \
    catkin build aerial_robot --no-status
