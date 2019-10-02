1 JetPack-L4T-3.3-linux-x64_b39,host上没全装，或者基本没装，jetson上也没装VisionWorks Pack and Compile CUDA Samples。

开设wifi时按照Jetson/TX1 WiFi Access Point https://elinux.org/Jetson/TX1_WiFi_Access_Point 打开后正常。

这个参数下次再恢复，就可以再连其他热点，否则只能自己作为热点。

2 jetson_ros_install.sh有修改

# 3 nodes

## vision
TrailNet view orientation and lateral offset 视方向和横向偏移
YOLO object detection 
DSO visual odometry: visual odometry component其输出被转换以摄像机为中心的深度地图，用于障碍物检测和回避。

GSCam: usb camera input
JOY:
MAVROS: communicate with px4

controller
resolving the ambiguity of needing to turn to correct an orientation error, and needing to fly in a non-straight path to correct a lateral offset error

# problem

trailnet_debug_gscam.launch no camera in rviz,but in rqt-image.
trailnet_debug_zed_gscam.launch 
no camera in rviz,but in rqt-image.
you pose
