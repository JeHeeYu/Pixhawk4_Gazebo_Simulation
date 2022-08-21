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

### Toolchain & ROS
<pre>
wget https://raw.githubusercontent.com/PX4/Devguide/master/build_scripts/ubuntu_sim_ros_melodic.sh
bash ubuntu_sim_ros_melodic.sh
</pre>
### MAVROS
<pre>
sudo apt-get update
sudo apt-get install ros-melodic-mavros ros-melodic-mavros-extras
wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
sudo bash ./install_geographiclib_datasets.sh   
sudo apt-get install python-catkin-tools python-rosinstall-generator -y

rosinstall_generator --rosdistro kinetic mavlink | tee /tmp/mavros.rosinstall
rosinstall_generator --upstream mavros | tee -a /tmp/mavros.rosinstall

// catkin Init
cd ~/catkin_ws
catkin init
wstool init src

// Work Path Depedancy
wstool merge -t src /tmp/mavros.rosinstall
wstool update -t src -j4
rosdep install --from-paths src --ignore-src -y
catkin build
</pre>
### MAVLINK
<pre>
sudo apt-get install python3-pip
pip3 install --user future
sudo apt-get install python3-tk
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
### GStreamer 
<pre>
apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
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
### Catkin workspace `/home/jhy/catkin_ws` is already initialized. No action taken.
　catkin init 오류
<pre>
catkin clean
catkin config --extend /opt/ros/melodic
</pre>
### error could not find a version that satisfies the requirement sympy
　requirements.txt 내 sympy version 오류
<pre>
vi /PX4-Autopilot/Tools/setup/requirements.txt
sympy delete
</pre>
### There already is a workspace config file .rosinstall at
<pre>
wstool update -j 4 -t src
</pre>
