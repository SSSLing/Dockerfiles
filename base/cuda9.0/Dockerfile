From nvidia/cudagl:9.0-devel-ubuntu16.04
MAINTAINER ling.shi

ENV CUDNN_VERSION 7.6.4.38
LABEL com.nvidia.cudnn.version="${CUDNN_VERSION}"

SHELL ["/bin/bash", "-c"]
RUN echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    apt-get update && \
# ----------------------------------------------------------------------------
# install cudnn7
    apt-get install -y --no-install-recommends libcudnn7=$CUDNN_VERSION-1+cuda9.0 libcudnn7-dev=$CUDNN_VERSION-1+cuda9.0 && \
    apt-mark hold libcudnn7 && \
    ln -s /usr/include/cudnn* /usr/local/cuda/include/ && \
    ln -s /usr/lib/x86_64-linux-gnu/libcudnn* /usr/local/cuda/lib64/ && \
    echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64" >> ~/.bashrc && \
    source ~/.bashrc && \
    rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/cuda.list* /etc/apt/sources.list.d/nvidia-ml.list*