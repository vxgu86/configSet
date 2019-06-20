

Ubuntu
如果用来做深度学习用，建议用16.04，GPU驱动比较成熟。
如果用来做其他opencv应用，则也可以用18.04。
同样适用于Jetson nano上的Ubuntu。

Python
可以用python3，也可以用python2.7，只是安装对应的库，并在构建虚拟环境时分别指定即可。

这里采用的是Ubuntu16.04+python3。

**1 安装OpenCV4依赖库**
升级下系统
``` bash
$ sudo apt-get update
$ sudo apt-get upgrade
```
安装开发工具
``` bash
$ sudo apt-get install build-essential cmake unzip pkg-config
```
安装图像/视频的I/O库，可以对磁盘中的媒体进行导入导出等。
``` bash
$ sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
```
安装GTK来得到图形界面。
``` bash
$ sudo apt-get install libgtk-3-dev
```
安装两个对OpenCV进行数学优化的库
``` bash
$ sudo apt-get install libatlas-base-dev gfortran
```
下面就是安装python3的开发头文件包。
``` bash
$ sudo apt-get install python3-dev
```

**2 安装OpenCV4依赖库**
