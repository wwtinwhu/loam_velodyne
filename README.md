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


