# Vision System

To use the camera setup a raspberry pi computer with a raspberry pi camera is currently required. 
This can be replaced with any ordinary camera if a wrapping ros publisher node is written.

## Instructions

The instructions to setup ROS on a raspberry pi can be found here [http://wiki.ros.org/indigo/Installation/UbuntuARM](http://wiki.ros.org/indigo/Installation/UbuntuARM).
Just install the binaries and you should be good to go. If you run into issues please make sure the camera is enabled. More on this topic here [https://www.raspberrypi.org/documentation/configuration/camera.md](https://www.raspberrypi.org/documentation/configuration/camera.md).

## The Camera Node

The instructions to setup the camera can be found at [https://github.com/UbiquityRobotics/raspicam_node](https://github.com/UbiquityRobotics/raspicam_node).
This has to be done on the raspberry pi.

### Modifications

There are some optional modifications that can be done. We lowered the resultion of the recordings to 600*600 as this gave satisfactory results and resulted in a higher throughput of frames per second.
This can be easily done in the provided launch files of the camera node mentioned above.

## Communication

To establish a connection between the the raspberry pi and the host computer that does all the image analysis a wired connection is recommended. The easiest setup is to have a router and connect both the raspberry pi and the host computer to it.
Otherwise a standard network cable can be used to establish the connection between the computers. Please refer to this guide for a how to [https://w3epic.com/setup-lan-connection-to-connect-between-two-ubuntu-12-systems/](https://w3epic.com/setup-lan-connection-to-connect-between-two-ubuntu-12-systems/).

## Final modifications

At the end the `/etc/hosts` file has to be modified. Add these lines to the file on the raspberry pi (make sure the IPs are correct):
```
127.0.0.1   rpi.local
192.168.0.2 mainpc.local
```
and something like this on the host computer:
```
127.0.0.1   mainpc.local
192.168.0.3 rpi.local
```

Finally create a file called `run_camera.sh` with the following contents:
```
export ROS_HOSTNAME=mainpc.local
export ROS_MASTER_URI=http://mainpc.local:11311

roslaunch raspicam_node camerav1_1280x720.launch
```
Please adjust the last line according to the appropirate launchfile (looking at camera version and resultion).

## Tips

- Make sure no X-Server is running. This can significantly impact the performance of the raspberry pi.
