FROM ros:noetic

# Install ROS Packages
RUN apt-get update && apt-get install -y \
    git \
    curl\
    ros-noetic-desktop-full \
    ros-noetic-moveit \
    ros-noetic-catkin \
    python3-catkin-tools \
    python3-wstool

# Setup LCAS User
RUN useradd -rm -d /home/lcas -s /bin/bash -g root -G sudo -u 1001 lcas
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# RUN echo "source /usr/share/gazebo/setup.bash" >> /home/lcas/.bashrc \
#     && echo "source /opt/ros/humble/setup.bash" >> /home/lcas/.bashrc

RUN mkdir -p /home/lcas/ws/
RUN ln -s /workspaces/CMP9764/src /home/lcas/ws/src

# WORKDIR /home/lcas/ws/moveit
# RUN git clone https://github.com/ros-planning/moveit_tutorials.git -b master
# RUN git clone https://github.com/ros-planning/panda_moveit_config.git -b noetic-devel

# RUN wstool init .
# RUN wstool merge -t . https://raw.githubusercontent.com/ros-planning/moveit/master/moveit.rosinstall
# RUN wstool remove moveit_tutorials  # this is cloned in the next section
# RUN wstool update -t .

# RUN rosdep install -y --from-paths . --ignore-src --rosdistro noetic
# RUN catkin config --extend /opt/ros/noetic --cmake-args -DCMAKE_BUILD_TYPE=Release
# # RUN cat /home/lcas/ws/moveit/devel/setup.bash >> /home/lcas/.bashrc

# add commit history to bust cache if and when needed.
ADD "https://api.github.com/repos/LCAS/cmp9764/commits?per_page=1&sha=main" .lcas_addons.commits
