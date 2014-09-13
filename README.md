INSTALL
-------
sudo apt-get update  
sudo apt-get upgrade  
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'  
wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -  
sudo apt-get update  
sudo apt-get install ros-indigo-desktop-full  
sudo rosdep init  
rosdep update  
echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc  
source .bashrc  
sudo apt-get install python-rosinstall  
mkdir -p ~/catkin_ws/src  
cd ~/catkin_ws/src  
catkin_init_workspace  
cd ~/catkin_ws  
catkin_make  
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc  
cd  
source .bashrc  
cd ~/catkin_ws  
sudo apt-get install ros-indigo-joystick-drivers  
sudo apt-get install xboxdrv  
cd /tmp  
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.13.11.4-trusty/linux-headers-3.13.11-03131104-generic_3.13.11-03131104.201406201536_amd64.deb  
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.13.11.4-trusty/linux-headers-3.13.11-03131104_3.13.11-03131104.201406201536_all.deb  
wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.13.11.4-trusty/linux-image-3.13.11-03131104-generic_3.13.11-03131104.201406201536_amd64.deb  
sudo dpkg -i linux-headers-3.13*.deb linux-image-3.13*.deb  
sudo reboot  
cd ~/catkin_ws/src  
git clone https://github.com/occominc/ardrone_joystick.git  
git clone https://github.com/occominc/autonavx_ardrone.git  
git clone https://github.com/occominc/tum_simulator.git  
git clone https://github.com/AutonomyLab/ardrone_autonomy.git -b indigo-devel  
git clone https://github.com/ros-simulation/gazebo_ros_pkgs.git -b indigo-devel  
sudo apt-get install ros-indigo-gazebo-ros-pkgs ros-indigo-gazebo-ros-control  
rosdep update  
rosdep check --from-paths . --ignore-src --rosdistro indigo  
rosdep install --from-paths . --ignore-src --rosdistro indigo -y  
cd ~/catkin_ws  
catkin_make  

START FOR PHYSICAL DRONE
------------------------
open five tabs, in each one run a separate command in this order:  
1) roscore  
2) rosrun ardrone_autonomy ardrone_driver  
3) rosrun rviz rviz (add an Image with Topic == /ardrone/image_raw)  
4) rosparam set joy_node/dev "/dev/input/js1"; rosrun joy joy_node  
5) rosrun ardrone_joystick ardrone_teleop  

START FOR VIRTUAL DRONE
------------------------
open five tabs, in each one run a separate command in this order:  
1) roscore  
2) rosrun rviz rviz (add an Image with Topic == /ardrone/image_raw)  
3) rosparam set joy_node/dev "/dev/input/js1"; rosrun joy joy_node  
4) rosrun ardrone_joystick ardrone_teleop  
5) roslaunch cvg_sim_gazebo ardrone_testworld.launch  
