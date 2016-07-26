FROM ros:indigo-ros-core
RUN echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
RUN apt-get update && exec apt-get install -y \
        ros-indigo-slam-gmapping \
        ros-indigo-amcl \
        ros-indigo-map-server \
        ros-indigo-move-base \
        ros-indigo-navigation

RUN echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc

COPY ./lib/*.sh /
RUN chmod 755 /*.sh
COPY ./lib/*.launch /
