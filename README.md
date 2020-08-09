# Dense Mapping

his repo is forked from [DenseSurfelMapping](https://github.com/HKUST-Aerial-Robotics/DenseSurfelMapping), aiming to learn surfel and run it successfully.  

<p align="center">
<img src="fig/example2.png" alt="mapping example" width = "465" height = "300">
</p>

# Software

The open-sourced surfel fusion system is used for reconstructing the KITTI dataset using ORB_SLAM2. For VINS-MONO, we are using it in a [teach-and-repeat project](https://www.youtube.com/watch?v=ehoJi4K_QKE) and will opensource lately. This project consists of three parts: the surfel_fusion, a modified ORB_SLAM2, and a kitti publisher.

## ORB_SLAM2
The ORB_SLAM2 is from the original [one](https://github.com/raulmur/ORB_SLAM2) and is modified to publish necessary information. You may install the ORB_SLAM2 following the original instructions.

## Surfel_fusion
Surfel_fusion can be installed in ros catkin workspace by 
```
catkin_make
```

## Kitti publisher
kitti publisher is a simple python warper to publish the Kitti dataset along with the pre-calculated depth maps (using [PSMNet](https://github.com/JiaRenChang/PSMNet)).

# Data

Here, we provide sequence 00 from the kitti dataset so that you can easily run the code. You can download the dataset from [this_link](https://www.dropbox.com/s/qpn40yt8bjvkapd/kitti_sequence_00.tar.gz?dl=0).

# Run the code
If you have installed all three components from the software

1. change line 23 in ```./kitti_publisher/scripts/publisher.py``` according to your downloaded dataset path.

2. change the path ```/home/wang/software/ORB_SLAM2/Vocabulary/ORBvoc.txt``` and ```/home/wang/software/ORB_SLAM2/Examples/Stereo/KITTI00-02.yaml``` in ```/ORB_SLAM2/orb_kitti_launch.sh``` according to your environment.

3. open four terminal windows: run the ORB_SLAM2 by

```
./orb_kitti_launch.sh 
```

, run the surfel fusion by

```
roslaunch surfel_fusion kitti_orb.launch
```

, and run the kitti publisher by

```
rosrun kitti_publisher publisher.py
```

, and run the rviz by

```
rviz
```
(you can load the rviz_config.rviz in the project to load published messages).

4. the kitti publisher will initialize a window and you can start the publisher by press any key on that window. Press ***Esc*** will quit the publisher.

# Save the result
The code also supports saving the reconstructed model by changing line 22 in ```/surfel_fusion/launch/kitti_orb.launch```. Just press crtl+c on surfel fusion will cause the software to save meshes into the defined the path and quit the process. You can view the saved mash using [CloudCompare](https://www.danielgm.net/cc/) or other softwares.
