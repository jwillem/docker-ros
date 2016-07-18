#!/bin/bash
set +e
/wait-for-it.sh --timeout=5 master:11311
if [[ $? == 0  ]]; then
  source "/opt/ros/indigo/setup.bash"
  /bin/bash -c "roslaunch p2os_launch pioneerMasterLaunchFile.launch" 2>&1 &
  /bin/bash -c "rostopic pub /cmd_motor_state p2os_msgs/MotorState 1" 2>&1 &
  while true
  do
    sleep 1
  done
else
  echo "Error with master!"
fi
