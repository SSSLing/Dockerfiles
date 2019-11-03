From nvidia/cudagl:9.0-devel-ubuntu16.04
MAINTAINER ling.shi

ENV CUDNN_VERSION 7.5.1.10
LABEL com.nvidia.cudnn.version="${CUDNN_VERSION}"

SHELL ["/bin/bash", "-c"]
RUN apt-get update && \
# ----------------------------------------------------------------------------
# install cudnn7
    apt-get install -y --no-install-recommends libcudnn7=$CUDNN_VERSION-1+cuda9.0 libcudnn7-dev=$CUDNN_VERSION-1+cuda9.0 && \
    apt-mark hold libcudnn7 && \
    ln -s /usr/include/cudnn* /usr/local/cuda/include/ && \
    ln -s /usr/lib/x86_64-linux-gnu/libcudnn* /usr/local/cuda/lib64/ && \
    echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64" >> ~/.bashrc && \
    source ~/.bashrc && \
    apt-get install -y python && \
    apt-get install -y python-pip && \
    pip2 install tensorflow-gpu==1.12.0 && \
    rm -rf /var/lib/apt/lists/*