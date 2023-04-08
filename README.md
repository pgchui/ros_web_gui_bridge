## ROS websocket and nipplejs
[tutorial](https://www.ross-robotics.co.uk/news/w79zhjoey8k0univkzvr1qyqorgqbf)
### Run:
```
roslaunch ros_gui_bridge websocket.launch
```

## Using UVC camera with "libuvc_camera" package
[tutorial](https://www.ross-robotics.co.uk/news/ros-web-tutorial-part-2-working-with-cameras)
1. Find vendor id and product id using `udevadm info --name=/dev/video1 --attribute-walk` \
For Thinkpad X1 Extreme Gen1, for cameras are listed using `ls /dev/video*`. They are "video[0:4]" where "video0" and "video1" are dedicated to integrated video camera and "video2" and "video3" are dedicated to integrated IR camera. "video1" is the one you want to use and "video0" provides metadata about the video data [(source)](https://unix.stackexchange.com/questions/512759/multiple-dev-video-for-one-physical-device)
2. Use `v4l2-ctl --list-formats-ext -d /dev/video0` to check the metadata including width, length, frame rate, and pixel format.
3. By default, $USER has to privilege to access the integrated camera. So adding privilege is needed [(source)](https://stackoverflow.com/a/34702977) by `sudo chmod a+w /dev/bus/usb/001/003`.
### Run:
```
roslaunch ros_gui_bridge camera.launch
```

## Running video server using "web_video_server" package
[tutorial](https://www.ross-robotics.co.uk/news/ros-web-tutorial-part-3-web-video-server)
### Run:
1. run server:
```
rosrun web_video_server web_video_server
```
2. visit [http://0.0.0.0:8080](http://0.0.0.0:8080)
3. set parameters: [http://0.0.0.0:8080/stream?topic=/image_raw&type=mjpeg&quality=10&invert&width=640&height=400&default_transport=compressed](http://0.0.0.0:8080/stream?topic=/image_raw&type=mjpeg&quality=10&invert&width=640&height=400&default_transport=compressed)