ARG from
FROM ${from}
MAINTAINER ling.shi

SHELL ["/bin/bash", "-c"]
RUN rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/cuda.list* /etc/apt/sources.list.d/nvidia-ml.list* && \
    apt-get update && \
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
# # install python3.6.10
ADD software/Python-3.6.10.tar.xz /home/software/
RUN cd /home/software/Python-3.6.10 && \
    ./configure && \
    make && \
    make install
RUN python -m pip install -i https://mirrors.aliyun.com/pypi/simple/ -U pip && \
    python3 -m pip install -i https://mirrors.aliyun.com/pypi/simple/ -U pip setuptools && \
    python -m pip install -i https://mirrors.aliyun.com/pypi/simple/ pandas && \
    python3 -m pip install -i https://mirrors.aliyun.com/pypi/simple/ numpy \
                                                                      scipy \
                                                                      pyyaml \
                                                                      rospkg \
                                                                      numba \
                                                                      fire \
                                                                      pybind11 \
                                                                      tensorboardX \
                                                                      scikit-image \
                                                                      shapely \
                                                                      matplotlib
# # ----------------------------------------------------------------------------
# # install nlopt
# # ADD https://codeload.github.com/stevengj/nlopt/tar.gz/v2.5.0 /home/software/
# ADD software/nlopt-2.5.0.tar.gz /home/software/
# RUN cd /home/software && \
#     # tar -zxvf nlopt-2.5.0.tar.gz && \
#     cd nlopt-2.5.0 && \
#     mkdir build && \
#     cd build && \
#     cmake ../ && \
#     make && \
#     make install
# # ----------------------------------------------------------------------------
# # install Ceres Solver
# # ADD http://ceres-solver.org/ceres-solver-1.14.0.tar.gz /home/software/
# ADD software/ceres-solver-1.14.0.tar.gz /home/software/
# RUN cd /home/software && \
#     apt-get install -y cmake && \
#     apt-get install -y libgoogle-glog-dev && \
#     apt-get install -y libatlas-base-dev && \
#     apt-get install -y libeigen3-dev && \
#     apt-get install -y libsuitesparse-dev && \
#     # tar zxf ceres-solver-1.14.0.tar.gz && \
#     mkdir ceres-bin && \
#     cd ceres-bin && \
#     cmake ../ceres-solver-1.14.0 && \
#     make -j3 && \
#     make test && \
#     make install
# # ----------------------------------------------------------------------------
# # install qpOASES
# # ADD http://www.qpoases.org/go/release /home/software/
# ADD software/qpOASES-3.2.1.zip /home/software/
# RUN cd /home/software && \
#     unzip qpOASES-3.2.1.zip && \
#     cd qpOASES-3.2.1 && \
#     mkdir build && \
#     cd build && \
#     cmake ../ && \
#     make && \
#     make install
# # ----------------------------------------------------------------------------
# # install osqp
# # ADD https://dl.bintray.com/bstellato/generic/OSQP/0.5.0/osqp-0.5.0.tar.gz /home/software/
# ADD software/osqp-0.5.0.tar.gz /home/software/
# RUN cd /home/software && \
#     # tar zxf osqp-0.5.0.tar.gz && \
#     cd osqp-0.5.0 && \
#     mkdir build && \
#     cd build && \
#     cmake ../ && \
#     make && \
#     make install
# # # ----------------------------------------------------------------------------
# # install ipopt-3.12.13 & Blas & Lapack & ASL & Mumps
# # ADD https://www.coin-or.org/download/source/Ipopt/Ipopt-3.12.13.zip /home/software/
# ADD software/Ipopt-3.12.13.zip /home/software/
# RUN cd /home/software && \
#     unzip Ipopt-3.12.13.zip -d /usr/share/cppad_ipopt && \
#     cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Blas && \
#     ./get.Blas && mkdir -p build && cd build && \
#     ../configure --prefix=/usr/local --disable-shared --with-pic && \
#     make install -s && \
#     cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Lapack/ && \
#     ./get.Lapack && mkdir -p build && cd build && \
#     ../configure --prefix=/usr/local --disable-shared --with-pic --with-blas="/usr/local/lib/libcoinblas.a -lgfortran" && \
#     make install && \
#     cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/ASL/ && \
#     ./get.ASL && \
#     cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Mumps/ && \
#     ./get.Mumps && \
#     cd /usr/share/cppad_ipopt/Ipopt-3.12.13 && \
#     ./configure --prefix=/usr/local coin_skip_warn_cxxflags=yes --with-blas="/usr/local/lib/libcoinblas.a -lgfortran" --with-lapack=/usr/local/lib/libcoinlapack.a && \
#     make && make test && make install
# # ----------------------------------------------------------------------------
# # install ASL
# # ADD https://www.coin-or.org/download/source/BuildTools/BuildTools-ASL-1.0.7.zip /home/software/
# ADD software/ThirdParty-ASL.tar /home/software/
# RUN cd /home/software && \
#     cd ThirdParty-ASL && \
#     ./get.ASL && \
#     ./configure && \
#     make && \
#     make install
# # ----------------------------------------------------------------------------
# # install Mumps
# # ADD https://www.coin-or.org/download/source/BuildTools/BuildTools-Mumps-1.6.2.zip /home/software/
# ADD software/ThirdParty-Mumps.tar /home/software/
# RUN cd /home/software && \
#     cd ThirdParty-Mumps && \
#     ./get.Mumps && \
#     ./configure && \
#     make && \
#     make install
# # ----------------------------------------------------------------------------
# # install ipopt-3.13.1
# # ADD https://www.coin-or.org/download/source/Ipopt/Ipopt-3.13.1.zip /home/software/
# ADD software/Ipopt-3.13.1.zip /home/software/
# RUN export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib && \
#     source /root/.bashrc && \
#     cd /home/software && \
#     unzip Ipopt-3.13.1.zip && \
#     cd /home/software/Ipopt-releases-3.13.1 && \
#     ./configure && \
#     make && \
#     make test && \
#     make install
# ----------------------------------------------------------------------------
# install ipopt-3.13.1
ADD software/mxnet-horizon-1.5.1.1.1b20191230.tgz /home/software/
RUN cd /home/software && \
    pip3 install mxnet_horizon_cu92-1.5.1.1.1b20191230-py2.py3-none-manylinux1_x86_64.whl -i https://mirrors.aliyun.com/pypi/simple/
# ----------------------------------------------------------------------------
RUN rm -rf /home/software && \
    rm -rf /var/lib/apt/lists/*