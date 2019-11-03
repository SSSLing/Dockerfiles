ARG from
FROM ${from}
MAINTAINER ling.shi

ADD https://codeload.github.com/stevengj/nlopt/tar.gz/v2.5.0 /home/software/
ADD https://www.coin-or.org/download/source/Ipopt/Ipopt-3.12.13.zip /home/software/
ADD http://ceres-solver.org/ceres-solver-1.14.0.tar.gz /home/software/
ADD http://www.qpoases.org/go/release /home/software/
ADD https://dl.bintray.com/bstellato/generic/OSQP/0.5.0/osqp-0.5.0.tar.gz /home/software/

SHELL ["/bin/bash", "-c"]
RUN apt-get update && \
# ----------------------------------------------------------------------------
# install others
    apt-get install -y wget && \
    apt-get install -y net-tools && \
    apt-get install -y unzip && \
    apt-get install -y uuid-dev && \
    apt-get install -y cppad && \
    apt-get install -y protobuf-compiler && \
    apt-get install -y python && \
    apt-get install -y python-pip && \
    apt-get install -y python-pandas && \
    apt-get install -y python3 && \
    apt-get install -y python3-pip && \
    apt-get install -y python3-numpy && \
    apt-get install -y python3-scipy && \
# ----------------------------------------------------------------------------
# install libs
    apt-get install -y libbullet-dev && \
    apt-get install -y libglew-dev && \
    apt-get install -y libgoogle-glog-dev && \
    apt-get install -y libpcap-dev && \
    apt-get install -y libpng++-dev && \
    apt-get install -y libprotobuf-dev && \
    apt-get install -y libsdl-image1.2-dev && \
    apt-get install -y libv4l-dev && \
    apt-get install -y libzmq3-dev && \
# ----------------------------------------------------------------------------
# install sumo
    apt-get install -y software-properties-common python-software-properties && \
    add-apt-repository ppa:sumo/stable && \
    apt-get update && \
    apt-get install -y sumo sumo-tools && \
    echo "export SUMO_HOME=/usr/share/sumo" >> ~/.bashrc && \
    source ~/.bashrc && \
# ----------------------------------------------------------------------------
# install nlopt
    cd /home/software && \
    tar -zxvf v2.5.0 && \
    cd nlopt-2.5.0 && \
    mkdir build && \
    cd build && \
    cmake ../ && \
    make && \
    make install && \
# ----------------------------------------------------------------------------
# install ipopt & Blas & Lapack & ASL & Mumps
    cd /home/software && \
    unzip Ipopt-3.12.13.zip -d /usr/share/cppad_ipopt && \
    cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Blas && \
    ./get.Blas && mkdir -p build && cd build && \
    ../configure --prefix=/usr/local --disable-shared --with-pic && \
    make install -s && \
    cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Lapack/ && \
    ./get.Lapack && mkdir -p build && cd build && \
    ../configure --prefix=/usr/local --disable-shared --with-pic --with-blas="/usr/local/lib/libcoinblas.a -lgfortran" && \
    make install && \
    cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/ASL/ && \
    ./get.ASL && \
    cd /usr/share/cppad_ipopt/Ipopt-3.12.13/ThirdParty/Mumps/ && \
    ./get.Mumps && \
    cd /usr/share/cppad_ipopt/Ipopt-3.12.13 && \
    ./configure --prefix=/usr/local coin_skip_warn_cxxflags=yes --with-blas="/usr/local/lib/libcoinblas.a -lgfortran" --with-lapack=/usr/local/lib/libcoinlapack.a && \
    make && make test && make -j1 install && \
# ----------------------------------------------------------------------------
# install Ceres Solver
    cd /home/software && \
    apt-get install -y cmake && \
    apt-get install -y libgoogle-glog-dev && \
    apt-get install -y libatlas-base-dev && \
    apt-get install -y libeigen3-dev && \
    apt-get install -y libsuitesparse-dev && \
    tar zxf ceres-solver-1.14.0.tar.gz && \
    mkdir ceres-bin && \
    cd ceres-bin && \
    cmake ../ceres-solver-1.14.0 && \
    make -j3 && \
    make test && \
    make install && \
# ----------------------------------------------------------------------------
# install qpOASES
    cd /home/software && \
    unzip release && \
    cd qpOASES-3.2.1 && \
    mkdir build && \
    cd build && \
    cmake ../ && \
    make && \
    make install && \
# ----------------------------------------------------------------------------
# install osqp
    cd /home/software && \
    tar zxf osqp-0.5.0.tar.gz && \
    cd osqp-0.5.0 && \
    mkdir build && \
    cd build && \
    cmake ../ && \
    make && \
    make install && \
# ----------------------------------------------------------------------------
    rm -rf /home/software && \
    rm -rf /var/lib/apt/lists/*