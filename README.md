# loam_velodyne

This repository is forked from [laboshinl](https://github.com/laboshinl/loam_velodyne), which is a refactoring version of the [JiZhang's public code](http://docs.ros.org/indigo/api/loam_velodyne/html/files.html)

![Screenshot](/capture.bmp)

## Running

```
roslaunch loam_velodyne loam_velodyne.launch
```

In second terminal play sample velodyne data
```
rosbag play ~/Downloads/velodyne.bag 
```

Or read from velodyne VLP16 sample pcap
```
roslaunch velodyne_pointcloud VLP16_points.launch pcap:="$HOME/Downloads/velodyne.pcap"
```

## New : Save Global Map
When the slam mission is done or the bag is played over, you can use following order to save the global map and trajectory(aft_mapped_to_init)
```
rosbag play senMapOrder.bag --clock
```
Specific Code is in the LaserMapping::mapOrderHandeler

## Some Issues:
1. In rviz, the frame "camera_init" z axis points forward, which is incompatible with regularity, so should choose the base_link to display, but the camera_init can't transform to the base_link
```
<node pkg="tf" type="static_transform_publisher" name="base_link_to_camera" args="0 0 0 -1.570795 -1.570795 0        /camera /base_link   10" />
```
The code above can work when I roslaunch another project which has base_link, confusing

2.In LaserOdometry.cpp, I can't find the assignment of the variable of _ioRatio, so how this code below works?
 ```
 if (_ioRatio < 2 || frameCount() % _ioRatio == 1)  

 ```

