FROM lcas.lincoln.ac.uk/lcas/devcontainer/ros2-teaching:2324-devel

# Install OS Packages etc
RUN sudo apt-get update && sudo apt-get install -y \
    git \
    curl \
    wget 

RUN sudo apt install python3-rosdep

RUN sudo rosdep init -y
RUN rosdep update -y
RUN sudo apt update -y

RUN mkdir -p /workspaces/CMP9764/ws_moveit2/
RUN cd /workspaces/CMP9764/ws_moveit2/

RUN git clone --branch humble https://github.com/ros-planning/moveit2_tutorials

RUN sudo apt update -y && rosdep install -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO -y

RUN colcon build --parallel-workers 1  

RUN echo 'source /workspaces/CMP9764/ws_moveit2/install/setup.bash' >> ~/.bashrc

# add commit history to bust cache if and when needed.
ADD "https://api.github.com/repos/LCAS/cmp9764/commits?per_page=1&sha=main" .lcas_addons.commits
