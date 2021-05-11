---
description: This page is under construction.
---

# Pre-setup

## Preliminaries

* [ ] Simulation: successful test of your own controller on [ROS/Gazebo](http://gazebosim.org/).
* [ ] Packages installed
  * Firefly OBC
    * [asctec\_mav\_framework](https://github.com/MRASL/asctec_mav_framework): framework for data aquisition and position control to be used with the highlevel \(HL\) processor of Ascending Technologies helicopters
    * [MSF](https://github.com/ethz-asl/ethzasl_msf): Modular framework for multi sensor fusion based  on an Extended Kalman Filter
    * Controller: in this tutorial, the [gain-scheduling controller](https://github.com/MRASL/gsft_control) will be tested
  * Remote Computer
    * [VRPN Client](/Equipment/Vicon/Usage): connects to the Vicon server through the Virtual Reality Peripheral Network; provides position, orientation, velocity and angular velocity.
* [ ] VICON setup: see our [Vicon page](../vicon/overview.md) for more detail.
* [ ] Power on
  * Firefly's FCU \(flight control unit\) with an ASCTEC battery fully charged \(5000 mAh, 11.1V\)
  * Firefly's On-Board Computer \(OBC\)

## Network

Remote monitoring and control the Firefly hexarotor UAV from a distance computer. In this tutorial, the desktop `L5816-18` and the object `firefly_blue` are used.

### **IP address**

The remote computer and the Firefly have to be connected to the **same network** \(MRASL\).  You can check your IP address by typing `ifconfig` in a terminal.

* The `firefly_blue` IP is [192.168.1.12](/Equipment/Networking/LAN.md). 
* For this tutorial assume that the remote computer IP is **192.168.1.4**. 

### **Remote monitoring and control of the Firefly from a distance computer**

* Check the connectivity between the remote computer and the `firefly_blue`  by running the following command in a remote computer terminal

  ```text
  $ ping 192.168.1.12
  ```

* To log into the Firefly's OBC we use the following commands

  ```text
  $ ssh asctec@192.168.1.12
  ```

  This command will open a ssh channel to the `firefly_blue` \(default password is `asctec`\). 

* If you are using the desktop L5816-18, you can also running the permanent _alias_ 

  ```text
  $ connect_firefly_blue
  ```

* We will use the `firefly_blue` as the ROS master, by setting the **ROS\_MASTER\_URI** and **ROS\_IP** variables to the drone's IP. To change the variables we use the following commands in the remote computer terminal

  ```text
  $ export ROS_MASTER_URI=http://192.168.1.12:11311
  $ export ROS_IP=192.168.1.4
  ```

  If you are using the desktop L5816-18, you can also running the permanent _alias_

  ```text
  $ master_firefly_blue
  ```

## ROS environment

Setting up the ROS environment: don't forget to run `$ source devel/setup.bash` in each terminal before continue with the following subsections. If you are using the the `firefly_blue` and the desktop L5816-18, you can also running the permanent _alias_ `$ gotien`.

### **Firefly's OBC**

* If you want to implement your own controller, you should list and kill all default nodes on OBC by running the following commands

  ```text
   $ rosnode list
   $ rosnode kill /AsctecProc
   $ rosnode kill /AutoPilot
  ```

* Running `/fcu`, `/mv_26805107` nodes \(Asctec Framework HL interface\) and `/pose_sensor` node \(MSF, private name\)

  ```text
  $ roslaunch asc_hl_interface fcu.launch
  $ roslaunch msf_updates viconpos_sensor.launch
  ```

### **Remote Computer**

* Running the `/firefly_blue/vrpn_client` node

  ```text
  $ roslaunch ros_vrpn_client mrasl_vicon.launch
  ```

  This launch file is a copy of the original `asl_vicon.launch`, using for the `firefly_blue` object and the Vicon server IP [192.168.1.200](/Equipment/Networking/LAN.md)

  ```text
  <arg name="object_name" default="firefly_blue" />
  <node ns="$(arg object_name)" name="vrpn_client" type="ros_vrpn_client" pkg="ros_vrpn_client" output="screen">
      <param name="vrpn_server_ip" value="192.168.1.200" />
  ```

After running these launch files, the `/pose_sensor` node may show this message \(OBC terminal\): `Pose measurement throttling is on, dropping messagesto be below 50.000000 Hz`.

