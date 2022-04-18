hri_skeletons
=============

A ROS node that detects and track human bodies in both 2D (2D keypoints of the 
body, in the image space) and 3D (generating on the fly URDF models for each 
detected humans, alongside their joint state and TF trees).

The detection relies on the open-source [Intel OpenVINO toolkit](https://docs.openvinotoolkit.org/),
requires only a RGB stream, and runs at ~15FPS on an Intel 10th gen CPU.


Installation
------------

- Follow first the general [ROS4HRI installation instructions](https://github.com/ros4hri/ros4hri/blob/master/README.md).

- Install the [`hri_msgs` package](https://github.com/ros4hri/hri_msgs/blob/master/README.md)

- pip3 install ikpy

- in your workspace, check that dependencies are installed
cd ~/my_ws && rosdep install -i --from-path src --rosdistro foxy -y

- then:

```
$ cd ~/src
$ git clone https://git.brl.ac.uk/ROS4HRI/hri_skeletons.git
$ cd hri_skeletons
$ mkdir build && cd build
$ cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=~/dev .. && make && make install
```

You can test this node by running:
```
$ ros2 run usb_cam usb_cam_node_exe
$ rosrun hri_skeletons run image:=/usb_cam/image_raw _debug:=true _model:=$HOME/openvino_models/public/human-pose-estimation-3d-0001/FP16/human-pose-estimation-3d-0001.xml
$ ros2 run rviz2 rviz2 # to visualize
```

which should display something like that (debug mode = true):

![debug visualisations](docs/debug_screenshot.jpg)

