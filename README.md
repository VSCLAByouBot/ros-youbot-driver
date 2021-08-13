# ros-youbot-driver

+ Ubuntu 18.04 LTS
+ ROS Melodic

## 01 | 建置 youBot driver 環境

### 1-1 安裝套件

   ```
   sudo apt-get install ros-melodic-pr2-msgs ros-melodic-brics-actuator ros-melodic-moveit git ros-melodic-ros-control ros-melodic-ros-controllers ros-melodic-joy ros-melodic-joystick-drivers ros-melodic-moveit-visual-tools python-rospkg libbluetooth-dev libcwiid-dev python-catkin-tools python3-catkin-pkg-modules python3-rospkg-modules python3-setuptools
   ```

### 1-2 建立 workspace

1. 複製所需 packages (此 repository)

   ```
   mkdir -p catkin_ws/src
   cd catkin_ws
   catkin_init_workspace
   cd src

   git clone https://github.com/youbot/youbot_driver.git
   cd youbot_driver
   git checkout hydro-devel
   cd ..

   git clone https://github.com/youbot/youbot_driver_ros_interface.git
   git clone https://github.com/youbot/youbot_description.git
   cd youbot_description
   git checkout kinetic-devel
   cd ..
   git clone https://github.com/youbot/youbot_navigation.git
   ```

2. 調整

   接著，修改 youbot_navigation/youbot_navigation_common 中的 CMakeLists.txt 檔案，在 target_link_libraries 之前加入以下內容：

   ```
   include_directories(${catkin_INCLUDE_DIRS})
   ```

3. 編譯

   ```
   cd ~/catkin_ws
   catkin build
   ```

   如此一來便完成建置。

## 02 | 執行（乙太連線）

1. 修改 youbot-ethercat.cfg 中的 ethernet device
2. 取得權限

   ```
   sudo setcap cap_net_raw+ep ~/catkin_ws/devel/.private/youbot_driver_ros_interface/lib/youbot_driver_ros_interface/youbot_driver_ros_interface
   sudo ldconfig /opt/ros/melodic/lib
   ```
3. 執行

   ```
   roslaunch youbot_driver_ros_interface youbot_driver.launch
   ```
