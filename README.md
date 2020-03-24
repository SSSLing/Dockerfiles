# 说明
- 为了扩展方便，把dockerfile拆分成三个部分
  - base：用来做基础镜像，安装一些除了ros以外的比较麻烦的东西，比如cuda、cudnn、tensorflow；如果并不需要用到这些，可以选择其他镜像作为基础镜像
  - ros-base：采用基础镜像，做一个包含ros-kinetic-desktop-full的ros的基础镜像；其中出于方便考虑，顺便安装了vim；
    - ros-pakeges：采用ros基础镜像，补充安装了一些pakege，如果并不需要用到，可以跳过这一镜像；
  - latest：主要大环境都安装完成后，有一些小环境和工具还要安装，就在这里进行安装，比如sumo交通流和各种优化器；文件里附带了一些开源工具，如果由于被墙了或者网络不给力，可以在dockerfile中直接使用软件包里的东西；
- 建议：如果要修改环境，可以拿ros-pakeges当基镜像；
- 如果需要使用宿主机Xserver运行rviz，需安装nvidia驱动的opengl（即安装驱动时不能加--no-opengl-files），然后在宿主机里依次执行以下指令：  
``` shell
root@root:/your/path# echo $DISPLAY #这个指令会显示现在使用的显示器编号，:0就表示是0号，:1就表示是1号，依次类推
:?
root@root:/your/path# xhost +local:root
root@root:/your/path# nvidia-docker run --rm -it \
                                        --env="DISPLAY" \
                                        --env="QT_X11_MITSHM=1" \
                                        --volume="/tmp/.X11-unix/X?:/tmp/.X11-unix/X?:rw" \
                                        runenv:?
#注意："/tmp/.X11-unix/X?:/tmp/.X11-unix/X?:rw"里的X?需要根据显示器编号更改，0号就写X0，1号就写X1，依次类推;runenv:?改成指定的版本
```
# base
- 基镜像：
  - nvidia/cudagl:9.0-devel-ubuntu16.04
- 软件依赖：
  - docker
  - nvidia docker
  - nvidia driver >= 384
- 安装：
  - cudnn 7.4.2.24
  - python2, python2-pip
  - tensorflow-gpu 1.12.0
# ros-base
- 基镜像：
  - runenv:base
- 软件依赖：
  - docker
  - 基镜像软件依赖
- 安装：
  - lsb-release
  - vim
  - ros-kinetic-desktop-full
## ros-pakeges
- 基镜像：
  - runenv:ros-base
- 软件依赖：
  - docker
  - 基镜像软件依赖
- 安装：
  - 一些ros pakege
# latest
- 基镜像：
  - runenv:ros-pakeges
- 软件依赖：
  - docker
  - 基镜像软件依赖
- 安装：
  - 一些lib
  - python2, python2-pip, pandas
  - python3, python3-pip, numpy, scipy
  - sumo
  - nlopt 2.5.0
  - Ipopt 3.12.13
  - Ipopt 3.13.1
  - Ceres 1.14.0
  - qpOASES 3.2.1
  - osqp 0.5.0