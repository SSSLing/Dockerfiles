ARG from
FROM ${from}
MAINTAINER ling.shi

SHELL ["/bin/bash", "-c"]
RUN apt-get update && \
# ----------------------------------------------------------------------------
# install others
    apt-get install -y wget \
                       net-tools \
                       unzip \
                       uuid-dev \
                       cppad \
                       protobuf-compiler \
                       python-pip \
# ----------------------------------------------------------------------------
# install libs
                       libbullet-dev \
                       libglew-dev \
                       libgoogle-glog-dev \
                       libpcap-dev \
                       libpng++-dev \
                       libprotobuf-dev \
                       libsdl-image1.2-dev \
                       libv4l-dev \
                       libzmq3-dev \
# ----------------------------------------------------------------------------
# install sumo
                       software-properties-common python-software-properties && \
    add-apt-repository ppa:sumo/stable && \
    apt-get update && \
    apt-get install -y sumo sumo-tools && \
    echo "export SUMO_HOME=/usr/share/sumo" >> ~/.bashrc && \
    source ~/.bashrc
# # ----------------------------------------------------------------------------
# install ipopt-3.12.13 & Blas & Lapack & ASL & Mumps
ADD software/Ipopt-3.12.13.zip /home/software/
RUN cd /home/software && \
    unzip Ipopt-3.12.13.zip -d /usr/share/cppad_ipopt && \
    cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Blas && \
    ./get.Blas && mkdir -p build && cd build && \
    ../configure --prefix=/usr/local --disable-shared --with-pic && \
    make install
RUN cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Lapack/ && \
    ./get.Lapack && mkdir -p build && cd build && \
    ../configure --prefix=/usr/local --disable-shared --with-pic && \
    make install
RUN cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/ASL/ && \
    ./get.ASL && \
    ./configure && \
    make && make install
RUN cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Mumps/ && \
    ./get.Mumps  && \
    ./configure && \
    make && make install && \
    cd /usr/share/cppad_ipopt/Ipopt-3.12.13 && \
    ./configure --prefix=/usr/local coin_skip_warn_cxxflags=yes && \
    make && make test && make install
# # ----------------------------------------------------------------------------
# # install ASL
# ADD software/ThirdParty-ASL.tar /home/software/
# RUN cd /home/software/ThirdParty-ASL && \
#     ./get.ASL && \
#     ./configure && \
#     make && \
#     make install
# # ----------------------------------------------------------------------------
# # install Mumps
# ADD software/ThirdParty-Mumps.tar /home/software/
# RUN cd /home/software/ThirdParty-Mumps && \
#     ./get.Mumps && \
#     ./configure && \
#     make && \
#     make install
# ----------------------------------------------------------------------------
# install ipopt-3.13.1
ADD software/Ipopt-3.13.1.zip /home/software/
RUN source /root/.bashrc && \
    cd /home/software && \
    unzip Ipopt-3.13.1.zip && \
    cd /home/software/Ipopt-releases-3.13.1 && \
    ./configure --prefix=/usr && \
    make && \
    make test && \
    make install
# ----------------------------------------------------------------------------
# install qpOASES
# ADD http://www.qpoases.org/go/release /home/software/
ADD software/qpOASES-3.2.1.zip /home/software/
RUN cd /home/software && \
    unzip qpOASES-3.2.1.zip && \
    cd qpOASES-3.2.1 && \
    mkdir build && \
    cd build && \
    cmake ../ && \
    make && \
    make install
# ----------------------------------------------------------------------------
# install nlopt
ADD software/nlopt-2.5.0.tar.gz /home/software/
RUN cd /home/software/nlopt-2.5.0 && \
    mkdir build && \
    cd build && \
    cmake ../ && \
    make && \
    make install
# ----------------------------------------------------------------------------
# install Ceres Solver
ADD software/ceres-solver-1.14.0.tar.gz /home/software/
RUN apt-get install -y cmake \
                       libgoogle-glog-dev \
                       libatlas-base-dev \
                       libeigen3-dev \
                       libsuitesparse-dev && \
    cd /home/software && \
    mkdir ceres-bin && \
    cd ceres-bin && \
    cmake ../ceres-solver-1.14.0 && \
    make && \
    make test && \
    make install
# ----------------------------------------------------------------------------
# install osqp
ADD software/osqp-0.5.0.tar.gz /home/software/
RUN cd /home/software/osqp-0.5.0 && \
    mkdir build && \
    cd build && \
    cmake ../ && \
    make && \
    make install
# # ----------------------------------------------------------------------------
# # install python-3.6.10
ADD software/Python-3.6.10.tar.xz /home/software/
RUN rm /usr/bin/lsb_release && \
    cd /home/software/Python-3.6.10 && \
    ./configure --prefix=/usr/local --enable-shared CFLAGS=-fPIC && \
    make && \
    make install
RUN python3 -m pip install -i https://mirrors.aliyun.com/pypi/simple/ -U pip setuptools && \
    pip3 install -i https://mirrors.aliyun.com/pypi/simple/ numpy \
                                                            pandas \
                                                            scipy \
                                                            pyyaml \
                                                            empy \
                                                            tqdm \
                                                            rospkg \
                                                            numba \
                                                            fire \
                                                            pybind11 \
                                                            tensorboardX \
                                                            scikit-image \
                                                            shapely \
                                                            matplotlib
# ----------------------------------------------------------------------------
# install mxnet-horizon-1.5.1.1
ADD software/mxnet-horizon-1.5.1.1.1b20191230.tgz /home/software/
RUN cd /home/software && \
    python3 -m pip install -i https://mirrors.aliyun.com/pypi/simple/ mxnet_horizon_cu100-1.5.1.1.1b20191230-py2.py3-none-manylinux1_x86_64.whl \
                                                                      tensorflow-gpu==1.15
# ----------------------------------------------------------------------------
RUN rm -rf /home/software && \
    rm -rf /var/lib/apt/lists/* /root/.cache/pip/*