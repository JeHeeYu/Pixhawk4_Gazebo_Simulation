# Pixhawk4 Gazebo Simulation
<br>
<br>

## Environment
　OS : Ubuntu.18.04
<br>
　ROS : Melodic
<br>
<br>
## Installation
### ROS Melodic
<pre>
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-get install curl # if you haven't already installed curl curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install ros-melodic-desktop-full

echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
source /opt/ros/melodic/setup.bash
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
sudo apt install python-rosdep
rosdep update
</pre>
### Gazebo
<pre>
sudo apt-get remove .*gazebo.*
sudo apt-get update && sudo apt-get install gazebo6
</pre>

### Toolchain & ROS
<pre>
wget https://raw.githubusercontent.com/PX4/Devguide/master/build_scripts/ubuntu_sim_ros_melodic.sh
bash ubuntu_sim_ros_melodic.sh
</pre>
### MAVROS
<pre>
sudo apt-get update
sudo apt-get install ros-melodic-mavros ros-melodic-mavros-extras
</pre>
### MAVLINK
<pre>
sudo apt-get install python3-pip
pip3 install --user future
sudo apt-get install python3-tk
mkdir mavlink
cd mavlink
git clone https://github.com/mavlink/mavlink.git --recursive
</pre>
　MAVLINk 관련 Install 후 Path 적용 필요
<pre>
vi ~/.bashrc

// 맨 하단에 추가
export PYTHONPATH=/home/jhy/mavlink
source ~/.bashrc 
echo $PYTHONPATH
</pre>
　mavlink Folder Path 적용
### PX4
<pre>
mkdir PX4
cd PX4
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
cd PX4-Autopilot
git pull
git submodule update
sudo apt-get upgrade libignition-math2
</pre>
### Python Package
<pre>
pip3 install empy
pip3 install --user pyros-genmsg
pip3 install --user toml
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
### EXCEPTION: Unable to start server[bind: Address already in use]. There is probably another Gazebo process running.
　Gazebo Process가 실행되어 있어 발생
<pre>
killall gzserver
</pre>
