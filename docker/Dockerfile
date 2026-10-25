	# ==============================================================================
# Base Image
# ==============================================================================
FROM ros:humble-ros-base-jammy

# ==============================================================================
# Arguments
# ==============================================================================
ARG USERNAME=dev
ARG UID=1000
ARG GID=1000

# Set default shell to Bash
SHELL ["/bin/bash", "-c"]

# ==============================================================================
# System Dependencies & ROS Packages
# ==============================================================================
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    nano \
    iputils-ping \
    net-tools \
    python3-colcon-common-extensions \
    python3-pip \
    python3-rosdep \
    ros-humble-demo-nodes-cpp \
    ros-humble-demo-nodes-py \
    ros-humble-rqt-graph \
    ros-humble-rviz2 \
    && rm -rf /var/lib/apt/lists/*

# ==============================================================================
# User Setup
# ==============================================================================
RUN groupadd -g ${GID} ${USERNAME} 2>/dev/null || true && \
    useradd -m -u ${UID} -g ${GID} -s /bin/bash ${USERNAME} && \
    echo "source /opt/ros/humble/setup.bash" >> /home/${USERNAME}/.bashrc && \
    echo "[ -f /ws/install/setup.bash ] && source /ws/install/setup.bash" >> /home/${USERNAME}/.bashrc

# ==============================================================================
# Entrypoint & Workspace Configuration
# ==============================================================================
COPY docker/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

USER ${USERNAME}
WORKDIR /ws

ENTRYPOINT ["/entrypoint.sh"]
CMD ["bash"]
