

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
安装开发工具(already installed in config of Jetson-nano-env.md)
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

**2 安装OpenCV4**
下载 [opencv](https://github.com/opencv/opencv) 和 [opencv_contrib](https://github.com/opencv/opencv_contrib) 。contrib repo包含一些额外的模块和函数。
``` bash
$ wget -O opencv.zip https://github.com/opencv/opencv/archive/4.1.0.zip
$ wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.1.0.zip
```
解压缩并重命名。
``` bash
$ unzip opencv.zip
$ unzip opencv_contrib.zip
$ mv opencv-4.0.0 opencv
$ mv opencv_contrib-4.0.0 opencv_contrib
```

以上情况处理结束之后，就可以创建虚拟环境并在其中安装OpenCV。

这部分可参见Jetson-nano-env.md中构建虚拟环境部分。

OpenCV依赖的库安装numpy，然后新建个build文件夹。
``` bash
$ workon cv
$ pip install numpy

$ cd ~/opencv
$ mkdir build
$ cd build
```
编译指令如下
``` bash
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D INSTALL_PYTHON_EXAMPLES=ON \
	-D INSTALL_C_EXAMPLES=OFF \
	-D OPENCV_ENABLE_NONFREE=ON \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
	-D PYTHON_EXECUTABLE=~/.virtualenvs/cvnano/bin/python \
	-D BUILD_EXAMPLES=ON ..
```

OPENCV_ENABLE_NONFREE一定要设置，设置之后才可以使用SIFT/SURF和一些专利保护的算法。
OPENCV_EXTRA_MODULES_PATH/PYTHON_EXECUTABLE这两个选项一定要改为自己的设置。


