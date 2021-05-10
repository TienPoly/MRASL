# Vicon object

## Vicon marker placement

Place at least three [markers](https://www.vicon.com/products/vicon-devices/markers-and-suits) on the object that you want to track.

![Good placement of markers](../.gitbook/assets/vicon_good_object-resized-1024.jpg)

![Bad placement of markers](../.gitbook/assets/vicon_bad_object-resized-1024.jpg)

{% hint style="info" %}
Why is the second marker placement \(4 markers\) not good? 

Answer: Due to symmetrical structure, Vicon can not distinguish the head and the tail of the object. The position is always good but the heading angle can be deviated by 180 deg.
{% endhint %}

## Create a Vicon object

* [ ] Place your robot \(with markers\) in the survey area
* [ ] Hold down the `Ctrl` key to select the markers that define the object and click `Create` in the `OBJECTS`tab.

![](../.gitbook/assets/vicon_object.png)

* [ ] You can also change the origin and the orientation of the object as documented [here](https://docs.vicon.com/display/Tracker33/About+the+Objects+tab). 

![](../.gitbook/assets/vicon_object_duckie3.png)

{% hint style="info" %}
Vicon uses the standard engineering coordinate system FLU: $$x$$axis - Forward \(Red\), $$y$$axis - Left \(Green\), $$z$$axis -Up \(Blue\).
{% endhint %}

## Tracking

Finally, you can track your object with Vicon and trace its pose

![Pose of the Active Wand ](../.gitbook/assets/vicon_tracking.png)

