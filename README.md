# ZED-ROS Guide
This repository contains a detailed guide on how to set up and work with the ZED camera using ROS. It includes steps to launch the ZED camera, enable object detection, record data using rosbag, and integrate RTAB-Map for SLAM.


### Note:
 - All the commands and guide were followed on **Ubuntu 20.04**.
 - Directory/file paths may vary.

## Prerequisites
Before starting, ensure you have the following tools installed:

- CUDA environment
- ROS (Robot Operating System)
- ZED SDK (version 4.1 or later)
- ZED ROS Wrapper
- Python 3.x ( most preferrable python versions are between 3.8 and 3.10)

## Setup
Building workplace:
```bash
cd ~/catkin_ws
catkin_make 
source devel/setup.bash
```

## ROS-ZED
To activate a command/file in Linux in the launch folder i.e. to set file permissions in the launch folder:
```bash
chmod +x [filename]
```

##  Launching the ZED Camera
```bash
cd ~/catkin_ws/src/zed-ros-wrapper/zed_wrapper/launch
roslaunch zed_wrapper zed2i.launch
```

### **Using RViz with ZED**
You can visualize the ZED camera feed with RViz by running:
```bash
rosrun rviz rviz
```

## To launch ZED camera with RViz
```bash
cd ~/catkin_ws/src/zed-ros-examples/zed_display_rviz/launch
roslaunch zed_display_rviz display_zed2i.launch
```

## **Object Detection in ZED ROS Wrapper**
To enable object detection in the ZED ROS wrapper, modify the `common.yaml` file:
```bash
cd ~/catkin_ws/src/zed-ros-wrapper/zed_wrapper/params/
nano common.yaml
```
- Change od_enabled to true:
```yaml
object_detection:
  od_enabled: true
```
- Save and close the file.

## Recording Data with ```rosbag```
Record ZED camera data with the following command:
### Steps to Record Data:
```bash
# rosbag record include-all-rostopics-that-are-used-in-ros-to-view-image-from-zed-camera
rosbag record /zed2i/zed_node/left/image_rect_color /zed2i/zed_node/point_cloud/cloud_registered /zed2i/zed_node/depth/depth_registered /zed2i/zed_node/pose /zed2i/zed_node/path_odom /zed2i/zed_node/path_map /zed2i/zed_node/mapping/fused_cloud /zed2i/zed_node/obj_det/objects /zed2i/zed_node/plane_marker
```

### Steps to Play Back the Recorded Data:
```bash
rosbag play your_recorded_data.bag
```

## Integrating RTAB-Map with ROS and ZED Camera
### Install RTAB-Map for ROS
```bash
sudo apt-get install ros-noetic-rtabmap-ros
```
### Launch RTAB-Map with ZED
```bash
cd ~/catkin_ws/src/zed-ros-examples/examples/zed_rtabmap_example/launch
roslaunch zed_rtabmap_example zed_rtabmap.launch
```
- In case of the error **RLException:** ```[zed_rtabmap.launch]``` is neither a launch file in package ```[zed_rtabmap_example]``` nor is ```[zed_rtabmap_example]``` a launch file name:

   - Source your workspace
```bash
source ~/catkin_ws/devel/setup.bash
```

## To check ROS related commands
```bash
cd ~/catkin_ws
rostopic list
```
### To use any command from rostopic
```bash
rostopic echo [topic-name-from-list]
```
**Explanation** 

```rostopic``` contains the rostopic command-line tool for displaying debug information about ROS Topics, including publishers, subscribers, publishing rate, and ROS Messages. It also contains an experimental Python library for getting information about and interacting with topics dynamically.</p>

## To use ZED tools and diagnostics
```bash
/usr/local/zed/tools/ZED_Explorer
/usr/local/zed/tools/ZED_Diagnostic
```

## Links
[Installation of ZED SDK](https://www.stereolabs.com/docs/installation)

[Installation of ROS-noetic](https://wiki.ros.org/noetic/Installation/Ubuntu)

[Getting Started with ROS and ZED](https://www.stereolabs.com/docs/ros)

