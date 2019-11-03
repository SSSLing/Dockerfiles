ARG from
FROM ${from}
MAINTAINER ling.shi

SHELL ["/bin/bash", "-c"]
RUN apt-get update && \
    apt-get install -y ros-kinetic-jsk-visualization && \
    apt-get install -y ros-kinetic-jsk-recognition && \
    apt-get install -y ros-kinetic-map-server && \
    apt-get install -y ros-kinetic-nmea-msgs && \
    apt-get install -y ros-kinetic-ompl && \
    apt-get install -y ros-kinetic-opencv3 && \
    apt-get install -y ros-kinetic-robot-localization && \
    apt-get install -y ros-kinetic-rosbridge-server && \
    apt-get install -y ros-kinetic-serial && \
    apt-get install -y ros-kinetic-tf2-sensor-msgs && \
    apt-get install -y ros-kinetic-unique-id && \
    apt-get install -y ros-kinetic-velodyne-msgs && \
    rm -rf /var/lib/apt/lists/*
