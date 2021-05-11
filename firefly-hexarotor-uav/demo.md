# Demo

### **Before running the controller**

* RVIZ and RQT
* Check our [Safety](/UAV/Safety) page
* Remote control
* Start the motors

### **Running the controller**

* Running the controller node by typing the following command in a Firefly's OBC terminal

  ```text
  $ source devel/setup.bash
  $ roslaunch gstf_control lqr_controller.launch
  ```

* Menu `Plugins/Introspection/Node Graph`: check node
* **Check the data before active the controller**

  Topic `/firefly/command/motor_speed/angular_velocities` and `/firefly/command/motor_speed/normalized` should **have to be `0.0` for all components**.

* Active the controller: change the remote control to autopilot

### **Send the reference** 

Menu `Plugins/Topics/Message Publisher`

* Add the topic `/firefly/command/pose` by using the button `+`
* Change the value of `pose/position/z` to `0.5`
* Check the box to publish

### **Verify the result** 

Menu `Plugins/Topics/Topic Monitor`

* Command: topic `/firefly/command/motor_speed/angular_velocities` and `/firefly/command/motor_speed/normalized`

## Example

{% embed url="https://youtu.be/8BS9n7uLMtI" %}



