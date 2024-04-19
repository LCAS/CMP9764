FROM lcas.lincoln.ac.uk/lcas/devcontainer/ros2-teaching:2324-devel

COPY .devcontainer/run.sh /root/
RUN chown root:root /root/run.sh
RUN chmod +x /root/run.sh
RUN bash -c "/root/run.sh"

RUN su lcas
RUN sudo chown -R lcas /opt/ros/lcas/
RUN sudo chmod 777 /opt/ros/lcas/install/setup.bash
RUN cat /opt/ros/lcas/install/setup.bash

RUN bash -c 'source /opt/ros/lcas/install/setup.bash'

# RUN bash -c 'ros2 topic list'

RUN sudo mkdir -p /ws_moveit2/src
COPY ./src /ws_moveit2/src
RUN sudo chown -R lcas /ws_moveit2/
RUN sudo chmod -R 777 /ws_moveit2/

RUN git clone --branch humble https://github.com/ros-planning/moveit2_tutorials /ws_moveit2/src/moveit2_tutorials/

# Install OS Packages etc
RUN sudo apt-get update && sudo apt-get install -y \
    git \
    curl \
    wget  \
    python3-rosdep \
    python3-vcstool \
    python3-colcon-common-extensions \
    python3-colcon-mixin \
    ros-humble-ament-cmake-python

RUN bash -c 'rosdep update -y'
RUN bash -c 'sudo apt update -y'
RUN bash -c 'cd /ws_moveit2'

RUN bash -c 'vcs import < /ws_moveit2/src/moveit2_tutorials/moveit2_tutorials.repos'

RUN bash -c 'rosdep install -r --from-paths /ws_moveit2/src/moveit2_tutorials --ignore-src --rosdistro $ROS_DISTRO -y'
# RUN bash -c 'colcon build --parallel-workers 1'

# add commit history to bust cache if and when needed.
ADD "https://api.github.com/repos/LCAS/cmp9764/commits?per_page=1&sha=main" .lcas_addons.commits
