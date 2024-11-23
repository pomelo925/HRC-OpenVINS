################################################################################################
# - Base stage
#   - This stage serves as the foundational stage for all other stages.
#   - Base image: OSRF ROS Humble Desktop Full
#       - https://hub.docker.com/r/osrf/ros/tags?page=1&name=humble-desktop-full
################################################################################################

FROM osrf/ros:humble-desktop-full AS base

LABEL org.opencontainers.image.title="OpenVINS Docker Image for HRC Lab"
LABEL org.opencontainers.image.authors="yoseph.huang@gmail.com"
LABEL org.opencontainers.image.licenses="MIT"
LABEL org.opencontainers.image.source="https://github.com/pomelo925/HRC-OpenVINS/blob/main/open_vins/docker/Dockerfile"

ARG USERNAME=user
ARG USER_UID=1000
ARG USER_GID=$USER_UID



################################################################################################
# - User Setup stage
#   - In this stage, I will create a non-root user and configure passwordless sudo.
################################################################################################
FROM base AS user-setup

## Create a non-root user
RUN groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /bin/bash && \
    apt-get update && \
    apt-get install -y sudo && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME && \
    rm -rf /var/lib/apt/lists/*



################################################################################################
# - Tools Installation stage
#   - In this stage, I will install convenient tools for development.
################################################################################################
FROM user-setup AS tools

## personal preference (optional)
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    nano \
    net-tools \
    ssh \
    x11-apps \ 
    && rm -rf /var/lib/apt/lists/*


## necessary packages
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    apt-utils \
    cmake \
    git \
    libatlas-base-dev \
    libceres-dev \
    libeigen3-dev \
    libgoogle-glog-dev \
    libgflags-dev \
    libsuitesparse-dev \
    python3-dev \
    python3-matplotlib \
    python3-numpy \
    python3-psutil \
    python3-tk \
    udev \
    usbutils \
    && rm -rf /var/lib/apt/lists/*



################################################################################################
# - Final stage
#   - In this stage, I will install required packages for Open-VINS.
#   - Reference:
#       - https://github.com/introlab/rtabmap_ros/tree/humble-devel?tab=readme-ov-file#installation
#       - https://github.com/introlab/rtabmap_ros.git
################################################################################################
FROM tools AS final



## 
#...
#...

## Set working directory
RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc


## Final configurations
# USER $USERNAME
CMD ["/bin/bash"]