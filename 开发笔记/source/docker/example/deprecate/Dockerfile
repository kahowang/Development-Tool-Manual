# >>> 基础镜像 >>>
FROM nvidia/cuda:11.2.1-devel-ubuntu20.04

# >>> 修改源，并安装apt包 >>>
RUN sed -i s@/archive.ubuntu.com/@/mirrors.gdut.edu.cn/@g /etc/apt/sources.list \
    && apt update \
    && DEBIAN_FRONTEND=noninteractive apt install -y \
        apt-utils \
        bash-completion \
        build-essential \
        ca-certificates \
        cmake \
        curl \
        git \
        keyboard-configuration \
        libx11-dev \
        locales \
        lsb-core \
        nano \
        net-tools \
        openssh-server \
        software-properties-common \
        vim \
        wget \
        gcc-9 g++-9 gcc-10 g++-10 \
    && rm -rf /var/lib/apt/lists/*

# >>> 安装ROS >>>
RUN DEBIAN_FRONTEND=noninteractive  sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list' \
    && apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 \
    && apt update \
    && DEBIAN_FRONTEND=noninteractive apt install -y ros-noetic-desktop-full \
    && echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc \
    && DEBIAN_FRONTEND=noninteractive apt install -y \
        python3-rosdep \
        python3-rosinstall \
        python3-rosinstall-generator \
        python3-wstool \
        python3-pip \
        && rm -rf /var/lib/apt/lists/*
 
# >>> 安装其他ros包依赖 >>>
RUN apt update \
    && DEBIAN_FRONTEND=noninteractive apt install -y \
        libboost-all-dev \
        libboost-python-dev \
        libeigen3-dev \
        libgeographic-dev \
        libglfw3-dev \
        libglm-dev \
        libgtest-dev \
        libpugixml-dev \
        python3-catkin-tools \
        libpcap-dev \
        ros-noetic-angles \
        ros-noetic-camera-info-manager \
        ros-noetic-ddynamic-reconfigure \
        ros-noetic-diagnostic-updater \
        ros-noetic-geodesy \
        ros-noetic-jsk-recognition-msgs ros-noetic-visualization-msgs \
        ros-noetic-lanelet2 \
        ros-noetic-nav-msgs \
        ros-noetic-nmea-msgs \
        ros-noetic-tf2-sensor-msgs \
    # catkin build的python依赖
    && rm -rf /var/lib/apt/lists/* \
    && pip3 install osrf-pycommon

# >>> 安装其他apt包依赖 >>>
RUN apt update \
    && DEBIAN_FRONTEND=noninteractive apt install -y \
        htop \
        wondershaper \
        ethstatus \
        cowsay \
    && rm -rf /var/lib/apt/lists/*

# >>> nvidia runtime>>>
# COPY --from=nvidia/opengl:1.2-glvnd-devel-ubuntu20.04\
#  /usr/local/lib/x86_64-linux-gnu \
#  /usr/local/lib/x86_64-linux-gnu
# 
# COPY --from=nvidia/opengl:1.2-glvnd-devel-ubuntu20.0 \
#  /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json \
#  /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json
# 
# RUN echo '/usr/local/lib/x86_64-linux-gnu' >> /etc/ld.so.conf.d/glvnd.conf && \
#  ldconfig && \
#  echo '/usr/local/$LIB/libGL.so.1' >> /etc/ld.so.preload && \
#  echo '/usr/local/$LIB/libEGL.so.1' >> /etc/ld.so.preload

# >>> nvidia-container-runtime >>>
ENV NVIDIA_VISIBLE_DEVICES ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

# >>> 安装gtsam,osqp,ceres >>>
RUN  cd /tmp \
    && git clone --depth=1 https://github.com/borglab/gtsam.git gtsam \
    && cd gtsam \
    && mkdir build && cd build && cmake .. \
    && make -j$(nproc) && make install \
    && DEBIAN_FRONTEND=noninteractive apt update \
    && apt install -y libgoogle-glog-dev libgflags-dev libatlas-base-dev libeigen3-dev libsuitesparse-dev \
    && wget -c http://ceres-solver.org/ceres-solver-2.0.0.tar.gz -O /tmp/ceres-solver-2.0.0.tar.gz \
    && cd /tmp \
    && tar -xzvf ceres-solver-2.0.0.tar.gz \
    && cd /tmp/ceres-solver-2.0.0 \
    && mkdir build && cd build && cmake .. \
    && make -j$(nproc) \
    && make install \
    && cd /tmp/ \
    && git clone --depth=1 --recursive https://github.com/osqp/osqp osqp \
    && cd osqp && mkdir build && cd build \
    && cmake .. \
    && make -j$(nproc) \
    && make install \
    && rm -rf /tmp/*

# >>> 安装anaconda >>>
# RUN wget -c https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh -O anaconda.sh \
#     && /bin/bash anaconda.sh -b -p /opt/conda \
#     && export "PATH=/opt/conda/bin:$PATH" \
#     && conda init \
#     && conda config --set auto_activate_base false \
#     && rm anaconda.sh

RUN pip3 install --no-cache-dir \
    catkin_pkg \
    netifaces \
    rospkg \
    defusedxml \
    easydict \
    empy \
    fire \
    gdown \
    matplotlib \
    opencv-python \
    pandas \
    pygeodesy \
    tqdm \
    pybind11[global] \
    && apt update \
    && DEBIAN_FRONTEND=noninteractive apt install -y \
        python3-pyqt5.qtserialport
        
# >>> 解决中文显示乱码问题 >>>
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# >>> 安装TensorRT >>>
#RUN cd /opt \
#    && gdown https://drive.google.com/uc?id=1MJdfsXaqBheYflwz2S56MiyQUcWlATA- \
#    && tar -xzvf TensorRT-7.2.3.4.Ubuntu-18.04.x86_64-gnu.cuda-11.1.cudnn8.1.tar.gz \
#    && rm TensorRT-7.2.3.4.Ubuntu-18.04.x86_64-gnu.cuda-11.1.cudnn8.1.tar.gz \
#    && echo 'export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/opt/TensorRT-7.2.3.4/lib' >> ~/.bashrc

# >>> 安装TensorRT >>>
# wget -c "https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin"
# mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
# apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub
# add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"
# apt install -y libnvinfer8 libnvonnxparsers8 libnvparsers8 libnvinfer-plugin8
# apt install -y libnvinfer-dev libnvonnxparsers-dev libnvparsers-dev libnvinfer-plugin-dev

# >>> 安装cudnn >>>
#RUN cd /opt \
#    && gdown https://drive.google.com/uc?id=157IFNclCOMb25mOFSqWugG_wCAr1IUTr \
#    && tar -xzvf cudnn-11.3-linux-x64-v8.2.1.32.tgz \
#    && cp cuda/include/cudnn*.h /usr/local/cuda/include \
#    && cp -P cuda/lib64/libcudnn* /usr/local/cuda/lib64 \
#    && chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn* \
#    && rm cudnn-11.3-linux-x64-v8.2.1.32.tgz \
#    && rm -rf cuda



# TensorRT 7.2.3
wget -c "https://developer.download.nvidia.com/compute/machine-learning/tensorrt/secure/7.2.3/local_repos/nv-tensorrt-repo-ubuntu1804-cuda11.1-trt7.2.3.4-ga-20210226_1-1_amd64.deb?dKkoOObf-ul4JqEMSSk7DkwlQB_4Cnc-xbshUMCcXHOfTIppHOOHofGxpLG8I7eiy0WLxMQL7DeVrWqsY8tcw5lthFKkNj81OBDTd4q0mgnv3BUgA1zFGQuSO0LCjwJ6nBb-eLyaGn-XuoZeOUM9KBrlz5tOfrlN8xjA8QfnEnET2l_PwIgUXreP63C4gB5WLFMJjk1ssJXrau-_Tz_Cpi75JYGOCREHEjGnckt_K0IfT4q9aajzVmFRoWsyxgL7sZrB&t=eyJscyI6ImdzZW8iLCJsc2QiOiJodHRwczpcL1wvd3d3Lmdvb2dsZS5jb20uaGtcLyIsIm5jaWQiOiJhZm0tY2hzLTQ0MjcwIn0"


# >>> 从当前目录导入文件 >>>
# COPY tmp /home/sleipnir/application    

# >>> 设置入口位置 >>>
# WORKDIR /home/sleipnir

# >>> 入口点函数 >>>
ENTRYPOINT ["/bin/bash"]    
