FROM osrf/ros:noetic-desktop-full

SHELL ["/bin/bash", "-c"]

RUN apt update && \
    apt install -y -q wget sudo lsb-release gnupg git sed build-essential && \
    source /opt/ros/noetic/setup.bash && \
    mkdir -p ~/ros/jsk_aerial_robot_ws/src && \
    cd ~/ros/jsk_aerial_robot_ws && \
    apt install -y python3-wstool python3-catkin-tools && \
    wstool init src && \
    wstool set -u -y -t src jsk_aerial_robot http://github.com/jsk-ros-pkg/jsk_aerial_robot --git && \
    wstool merge -t src src/jsk_aerial_robot/aerial_robot_${ROS_DISTRO}.rosinstall && \
    wstool update -t src && \
    rosdep install -y -r --from-paths src --ignore-src --rosdistro $ROS_DISTRO && \
    source /opt/ros/noetic/setup.bash && \
    catkin build && \
    echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc && \
    echo "source ~/ros/jsk_aerial_robot_ws/devel/setup.bash" >> ~/.bashrc && \
    echo "export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0" >> ~/.bashrc
