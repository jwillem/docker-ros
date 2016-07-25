FROM osrf/ros:indigo-desktop-full
RUN echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list
RUN echo "deb http://us.archive.ubuntu.com/ubuntu/ precise-updates main restricted" | sudo tee -a /etc/apt/sources.list.d/precise-updates.list
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
RUN apt-get update && exec apt-get install -y \
        ros-indigo-navigation \
        ros-indigo-nav2d \
	ros-indigo-turtlebot-bringup \
	python-pip \
	python-dev \ 
	openssh-server

RUN pip install shapely
RUN mkdir /var/run/sshd
RUN echo 'root:p' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
ENV ROS_MATER_URI=http://master:11311
ENV LC_ALL="C"

EXPOSE 22

# Setup catkin workspace
RUN echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
RUN bin/bash -c "source /opt/ros/indigo/setup.bash && \
                 mkdir -p ~/catkin_ws/src && \
                 cd ~/catkin_ws/src && \
                 catkin_init_workspace && \
		 cd ~/catkin_ws/src/heatmap && \
		 git checkout jade-devel && \
                 cd ~/catkin_ws/ && \
                 catkin_make"
RUN echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc

COPY ./lib/ssh-environment /root/.ssh/environment
RUN echo "PermitUserEnvironment=yes" >> /etc/ssh/sshd_config

COPY ./lib/*.sh /
RUN chmod 755 /*.sh
