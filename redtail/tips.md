TrailNet    

view orientation and lateral offset
视方向和横向偏移

object detection 

visual odometry component


ROSnode:
GSCam: usb camera input
JOY:
MAVROS: communicate with px4

vision
TrailNet 
YOLO
DSO visual odometry: 其输出被转换以摄像机为中心的深度地图，用于障碍物检测和回避。

controller
resolving the ambiguity of needing to turn to correct an orientation error, and needing to fly in a non-straight path to correct a lateral offset error
