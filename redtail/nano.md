# 1 image_publisher gscam
可以用gscam，但nano性能不够，波浪形。摄像头厂家说可以更改模式 YUV改为MJPG，尝试。

另外，以手机为热点hotpot时，nano与地面站都连，无法stream，目前没找到原因。

# 2 查看GPU情况 tegrastats

每个代表啥？

# mavros调试

直接用usb-ttl转换口接nano，收到的都是乱码，

 roslaunch mavros apm.launch fcu_url:="/dev/ttyTHS1:921600" gcs_url:="udp://@YOUR_GCS_IP"
 
后，再发

rosrun mavros mavsafety arm

没问题。需要花时间把ardupilot-redtail熟悉。



# 3 X-server尝试关掉



qmake: could not exec '/usr/lib/x86_64-linux-gnu/qt4/bin/qmake': No such file or dire

sudo apt-get install qt4-qmake


CMake Error at /usr/share/cmake-2.8/Modules/FindQt4.cmake:664 (message):
  Could NOT find QtCore.  
  
  apt-get install qt4-dev-tools


  
  
