# Control-Multi-Turtlebot3-by-Teleop

In this project I will run  multiple robots (turtlebot3) in gazebo and control them by teleop.

#### 1.Install necessary package 
```
$ sudo apt-get install ros-kinetic-multirobot-map-merge
```
#### 2.Load the robots in TurtleBot3 House
after install the package we need to load the 3 robots in TurtleBot3 House.
```
$ roslaunch turtlebot3_gazebo multi_turtlebot3.launch
```
These loaded turtlebot3s are set initial position and orientation. 

![3robots](https://user-images.githubusercontent.com/85634104/127886545-21222b26-97b9-4c7b-a489-0fe063ee63d7.png)

#### 3.Launch SLAM for each TurtleBot3
every command should be in new tab 
```
$ ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_0/base_footprint set_odom_frame:=tb3_0/odom set_map_frame:=tb3_0/map
$ ROS_NAMESPACE=tb3_1 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_1/base_footprint set_odom_frame:=tb3_1/odom set_map_frame:=tb3_1/map
$ ROS_NAMESPACE=tb3_2 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_2/base_footprint set_odom_frame:=tb3_2/odom set_map_frame:=tb3_2/map
```
#### 4.Merge map data from each TurtleBot3
in new tab
```
$ roslaunch turtlebot3_gazebo multi_map_merge.launch
```
#### 5.Run RViz
in new tab
```
$ rosrun rviz rviz -d `rospack find turtlebot3_gazebo`/rviz/multi_turtlebot3_slam.rviz
```
![3robotsRViz](https://user-images.githubusercontent.com/85634104/127886797-fb975a93-7422-456c-8990-517c8ac99cf1.png)

#### 6.Control The Robots
each command of these we should run it in new tab to contol each robot 
```
$ ROS_NAMESPACE=tb3_0 rosrun turtlebot3_teleop turtlebot3_teleop_key
$ ROS_NAMESPACE=tb3_1 rosrun turtlebot3_teleop turtlebot3_teleop_key
$ ROS_NAMESPACE=tb3_2 rosrun turtlebot3_teleop turtlebot3_teleop_key
```
after finishing ,this is the result in Rviz :

![3robotsRVisafter](https://user-images.githubusercontent.com/85634104/127887505-fd24db6a-096d-46d9-8b6d-51dae05d1de9.png)
#### 7.Save the map
now we need to save the map 
```
$ rosrun map_server map_saver -f ~/map
```

![multimap](https://user-images.githubusercontent.com/85634104/127887753-8d2dae03-6499-49dd-9f57-2fc79ca2be4f.png)




