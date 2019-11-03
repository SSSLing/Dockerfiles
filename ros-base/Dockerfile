ARG from
FROM ${from}
MAINTAINER ling.shi

SHELL ["/bin/bash", "-c"]
RUN apt-get update && \
    apt-get install -y lsb-release && \
    apt-get install -y vim && \
    sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' && \
    apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 && \
    apt-get update && \
    apt-get install -y ros-kinetic-desktop-full && \
    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc && \
    source ~/.bashrc && \
    rm -rf /var/lib/apt/lists/*
