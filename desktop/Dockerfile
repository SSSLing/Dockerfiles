ARG from
FROM ${from}
MAINTAINER ling.shi

SHELL ["/bin/bash", "-c"]
ADD debs/* /home/software/
RUN ln -s /usr/include/cudnn* /usr/local/cuda/include/ && \
    ln -s /usr/lib/x86_64-linux-gnu/libcudnn* /usr/local/cuda/lib64/ && \
    echo "export LD_LIBRARY_PATH=/usr/local/lib:/usr/lib:\$LD_LIBRARY_PATH:/usr/local/cuda/lib64" >> ~/.bashrc && \
    source ~/.bashrc && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    rm -rf /etc/apt/sources.list.d/cuda.list* /etc/apt/sources.list.d/nvidia-ml.list* && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y xfce4 && \
    dpkg -i /home/software/*.deb && \
    rm -rf /home/software /var/lib/apt/lists/*