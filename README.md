# soc-layers-spot
Applying ROS's social_naviagtion_layers plugin to rosbags in the SCAND dataset to detect the direction that humans are travelling towards in the scene. The social_navigation_layers plugin consists of a ProxemicLayer that adds a gaussian surface around the detected person and extends the gaussian surface in the direction that the person is moving in. The social_navigation_layers subscribes to the /people topic and requires a people detection algorithm to publish to the /people topic. Used https://github.com/yzrobot/online_learning for people detection.

<img width="511" alt="Screen Shot 2022-07-21 at 9 22 49 PM" src="https://user-images.githubusercontent.com/98352313/180348991-9ab3fe9f-a410-4c23-9f1c-d9625e212e4a.png">

# Install & Build
```
cd catkin_ws/src
git clone <repo link>
```
Follow Install & Build section and download required packages: https://github.com/yzrobot/online_learning

```
catkin build
```

# Run
```
cd catkin_ws
source devel/setup.bash
roslaunch spot_move_base spot_move_base_rosbag.launch
```
In a new terminal window:  
Go to workspace with people detection algorithm (https://github.com/yzrobot/online_learning)

```
source devel/setup.bash
roslaunch object3d_detector object3d_detector.launch
```
In RVIZ, add Map display for the costmap and Polygon display for robot footprint


https://user-images.githubusercontent.com/98352313/180490775-96105d61-7100-45eb-91a3-0dc3c3bc2f5f.mp4


# Parameters
Adjust parameters for the gaussian surface in spot_move_base/costmap_common_params.yaml
```
plugins:
- {name: social_layer, type: "social_navigation_layers::ProxemicLayer"}

social_layer:
  enabled: true
  cutoff: 125.0
  amplitude: 254
  covariance: 1.25
  factor: 5.0
  ```
# References

https://github.com/yzrobot/online_learning

https://github.com/DLu/navigation_layers

https://github.com/HareshKarnan/spot_move_base
