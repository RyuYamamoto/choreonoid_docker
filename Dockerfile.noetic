# syntax = docker/dockerfile:experimental
FROM osrf/ros:noetic-desktop

SHELL ["/bin/bash", "-c"]

RUN apt update && apt install -y --no-install-recommends \
		vim tmux git python3-pip python3-vcstool python3-catkin-tools

RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc

WORKDIR /root
RUN --mount=type=ssh \
    mkdir -m 0600 ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts \
    && git clone https://github.com/RyuYamamoto/choreonoid_ros_setup.git && cd choreonoid_ros_setup && mkdir src && vcs import src < choreonoid.repos \
    && ./src/choreonoid/misc/script/install-requisites-ubuntu-20.04.sh
WORKDIR /root/choreonoid_ros_setup
RUN /bin/bash -c 'source /opt/ros/noetic/setup.bash catkin config --cmake-args -DBUILD_CHOREONOID_EXECUTABLE=OFF -DCMAKE_BUILD_TYPE=Release && catkin build'

RUN echo "source /root/choreonoid_ros_setup/devel/setup.bash" >> ~/.bashrc

ENV NVIDIA_VISIBLE_DEVICES ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics
