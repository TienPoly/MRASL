# ROS environment

Setting up the ROS environment: don't forget to run `$ source devel/setup.bash` in each terminal before continue with the following subsections. If you are using the the `firefly_blue` and the desktop L5816-18, you can also running the permanent _alias_ `$ gotien`.

**Firefly's OBC**

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

**Remote Computer**

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

