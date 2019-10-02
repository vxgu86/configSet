1 JetPack-L4T-3.3-linux-x64_b39,host上没全装，或者基本没装，jetson上也没装VisionWorks Pack and Compile CUDA Samples。

开设wifi时按照Jetson/TX1 WiFi Access Point https://elinux.org/Jetson/TX1_WiFi_Access_Point 打开后正常。

这个参数下次再恢复，就可以再连其他热点，否则只能自己作为热点。

2 jetson_ros_install.sh有修改

# 3 nodes

## vision

caffe_ros ROS node has a parameter, camera_topic which can be used to change camera topic when running caffe_ros via rosrun or .launch file.

TrailNet view orientation and lateral offset 视方向和横向偏移
YOLO object detection 
DSO visual odometry: visual odometry component其输出被转换以摄像机为中心的深度地图，用于障碍物检测和回避。

GSCam: usb camera input
JOY:
MAVROS: communicate with px4

controller
resolving the ambiguity of needing to turn to correct an orientation error, and needing to fly in a non-straight path to correct a lateral offset error

# 4 problem

trailnet_debug_gscam.launch 跑起来后在rviz中打不开camera，能在rqt-image中看到，说明gscam是开了，只是与rviz中有问题。
trailnet_debug_zed_gscam.launch 的camera同样问题。
    <!-- Start the GSCAM node -->
    <node pkg="gscam" type="gscam" name="gscam">
        <!-- 
        To use just one sink (default):
        v4l2src device=$(arg device) ! video/x-raw, width=$(arg img_width), height=$(arg img_height) ! videoconvert

        To use 2 sinks (UDP H.265 streaming + ROS topic):
        v4l2src device=$(arg device) ! tee name=t ! queue ! videoconvert ! omxh265enc ! video/x-h265, stream-format=byte-stream ! h265parse ! rtph265pay config-interval=1 ! udpsink host=$(arg host_ip) port=6000 t. ! queue ! video/x-raw, width=$(arg img_width), height=$(arg img_height) ! videoconvert 
  
        -->
        <param name="gscam_config" value="v4l2src device=$(arg device) ! video/x-raw, width=$(arg img_width), height=$(arg img_height) ! videoconvert" />
        <param name="frame_id"        value="$(arg frame_id)" /> 
    </node>
env name="GSCAM_CONFIG" param name="gscam_config" 不影响
<param name="frame_id"        value="$(arg frame_id)" />  gscam加了这个参数后就可以看到pose。
