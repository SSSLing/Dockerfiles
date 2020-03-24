ARG from
FROM ${from}
MAINTAINER ling.shi

SHELL ["/bin/bash", "-c"]
RUN apt-get update && \
    apt-get install -y ros-kinetic-jsk-visualization \
                       ros-kinetic-jsk-recognition \
                       ros-kinetic-map-server \
                       ros-kinetic-nmea-msgs \
                       ros-kinetic-ompl \
                       ros-kinetic-opencv3 \
                       ros-kinetic-ros-numpy \
                       ros-kinetic-robot-localization \
                       ros-kinetic-rosbridge-server \
                       ros-kinetic-serial \
                       ros-kinetic-tf2-sensor-msgs \
                       ros-kinetic-unique-id \
                       ros-kinetic-velodyne-msgs \
                       ros-kinetic-velodyne-pointcloud && \
    rm -rf /var/lib/apt/lists/*