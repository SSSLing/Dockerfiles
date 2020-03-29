ARG from
FROM ${from}
MAINTAINER ling.shi

SHELL ["/bin/bash", "-c"]
ADD debs/turbovnc_2.2.4_amd64.deb /home/software/
ADD debs/virtualgl_2.6.3_amd64.deb /home/software/
RUN echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    rm -rf /etc/apt/sources.list.d/cuda.list* /etc/apt/sources.list.d/nvidia-ml.list* && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y xfce4 && \
    dpkg -i /home/software/*.deb && \
    rm -rf /home/software /var/lib/apt/lists/*