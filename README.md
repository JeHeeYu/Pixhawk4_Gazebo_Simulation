# Pixhawk4 Gazebo Simulation
<br>
<br>

## Environment
　OS : Ubuntu.18.04
　ROS : Melodic
<br>
<br>
## Installation
### Toolchain & ROS
<pre>
wget https://raw.githubusercontent.com/PX4/Devguide/master/build_scripts/ubuntu_sim_ros_melodic.sh
bash ubuntu_sim_ros_melodic.sh
</pre>
## Error Note
### Error in REST Request
　Gazebo Version에 관한 오류로 config.yaml 파일 수정 필요함
<pre>
cd /home/jhy/.ignition/fuel
vi config.yaml
</pre>
　config.yaml 내 url 수정
#### before
<pre>
---
# The list of servers.
servers:
  -
    name: osrf
    url: https://api.ignitionfuel.org

  # -
    # name: another_server
    # url: https://myserver

# Where are the assets stored in disk.
# cache:
#   path: /tmp/ignition/fuel

</pre>
#### after
<pre>
---
# The list of servers.
servers:
  -
    name: osrf
    url: https://api.ignitionrobotics.org

  # -
    # name: another_server
    # url: https://myserver

# Where are the assets stored in disk.
# cache:
#   path: /tmp/ignition/fuel

</pre>
