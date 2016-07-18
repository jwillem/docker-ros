FROM ros:indigo-ros-core
RUN echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
RUN apt-get update && exec apt-get install -y \
        ros-indigo-move-base \
        ros-indigo-navigation \
        ros-indigo-sicktoolbox* \
	ros-indigo-p2os-* \
	ros-indigo-pr2-* \
	ros-indigo-pr2-tele* \
        joystick

COPY ./lib/teleop_keyboard.launch /opt/ros/indigo/share/p2os_launch/launch/
COPY ./lib/pioneerMasterLaunchFile.launch /opt/ros/indigo/share/p2os_launch/launch/
COPY ./lib/tf_lrf_p2os.launch /opt/ros/indigo/share/p2os_launch/launch/
COPY ./lib/*.sh /
COPY ./lib/pioneer.launch /
RUN chmod 755 /*.sh
RUN echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
