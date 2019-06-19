# Jetson nano使用
## 概述

Jetson Nano是一款类似于树莓派的嵌入式高性能边缘AI设备，搭载四核Cortex-A57处理器，配备4GB LPDDR4内存，16GB的eMMC 5.1存储;配备Maxwell架构128 CUDA核心的GPU（被大型散热器覆盖），具备472 GFLOPS计算能力，支持4K 60Hz视频解码，可以以嵌入式形式加载到各种终端平台。

如此价位下并不包括全部所需的配件，以下是需要自己配置的：
micro-SD卡（最小 16GB，建议32GB micro-SD卡，安装配置环境的时候会下载很多东西）
5V 2.5A Micro USB电源
以太网电缆

这里有一些基本的[介绍](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit)，包括如何将系统img烧录到Sd卡的过程。
User Guide里建议烧录img后就刷机。

安装系统包和常用工具包
配置Python开发环境
在Jetson Nano上安装TensorFlow和Keras
安装Jetson推理引擎
更改默认摄像头
使用Jetson Nano进行分类和物体检测

## 安装系统包和常用工具包

在将img文件烧录之后，首先安装所需的系统包和常用工具包
``` bash
$ sudo apt-get install git cmake
$ sudo apt-get install libatlas-base-dev gfortran
$ sudo apt-get install libhdf5-serial-dev hdf5-tools
$ sudo apt-get install python3-dev
``` 

## 配置Python开发环境
** 奇怪 **
安装Python包管理器 pip，
看到python3 get-pip.py才意识到，可能是which python3

``` bash
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python3 get-pip.py
$ rm get-pip.py
``` 

使用Python virtual environments可保持多个Python开发环境相互独立，便于在一张SD卡上维护不同的开发环境 。

安装virtualenv和virtualenvwrapper管理Python虚拟环境，
``` bash
$ sudo pip install virtualenv virtualenvwrapper
``` 
更新 〜/ .bashrc文件，添加以下行：

``` bash
# virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
```

保存并退出编辑器，重新加载〜/ .bashrc文件 ：
``` bash
$ source ~/.bashrc
``` 
现在可以使用mkvirtualenv命令创建一个Python虚拟环境，命名虚拟环境为deep_learning，
``` bash
$ mkvirtualenv cvnano -p python3
``` 
## 安装TensorFlow和Keras

在Jetson Nano上安装TensorFlow和Keras之前，首先需要安装NumPy。

使用workon命令确保虚拟环境，然后安装NumPy：
``` bash
$ workon cvnano
$ pip install numpy
``` 
在Jetson Nano上安装NumPy需要大约10-15分钟的时间，因为它必须在系统上编译（目前没有用于Jetson Nano预构建版本的NumPy）。

下一步是在Jetson Nano上安装Keras和TensorFlow，这里不用pip installtensorflow-gpu。因为NVIDIA已经提供了[TensorFlow for Jetson Nano](https://devtalk.nvidia.com/default/topic/1048776/official-tensorflow-for-jetson-nano-/  )。
``` bash
$ pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v42 tensorflow-gpu==1.13.1+nv19.3
``` 
安装NVIDIA的 tensorflow-gpu软件包需要大约40分钟，其中有需要写权限的，我后来加了sudo。

最后一步是安装SciPy和Keras：

``` bash
$ pip install scipy
$ pip install keras
```

安装耗时约35分钟。

## 安装Jetson推理引擎
与Jetson tx2不同的是，Jetson Nano .img已经安装了JetPack，而tx2装好后只是一个纯净版的Ubuntu。

因此这里可以直接构建Jetson推理引擎，参见[编译Jetson-inference代码]（https://github.com/vxgu86/jetson-inference/blob/master/docs/%E7%BC%96%E8%AF%91Jetson-inference%E4%BB%A3%E7%A0%81.md）。

## 外接camera设置

使用NVIDIA Jetson Nano时有两种输入摄像头设备选项：

-- CSI相机模块，如Raspberry Pi camera模块
-- USB网络摄像头

这里以Logitech C920为例，它与Nano即插即用兼容。

在以camera为输入的例子中，DEFAULT_CAMERA值设置为 - 1，这表示使用的是CSI摄像头。如果使用USB摄像头，需要改变 DEFAULT_CAMERA为0（或任何正确的/dev/video V4L2摄像头）。

**我用的是1，0 不成功，不管板载的camera在不在**

``` bash
cd ~/jetson-inference/imagenet-camera
nano imagenet-camera.cpp
```

编辑C ++文件后需要重新编译，如下所示：

``` bash
cd ../build
make
sudo make install
```

make命令会重新编译已更改的文件，不会重新编译整个库。

编译结束后即可重新运行：

``` bash
cd aarch64/bin/
./imagenet-camera
```

图像分类模型在Jetson Nano上对从摄像头输入的1280×720的运行速度差不多在10 FPS，同样分辨率的物体检测可运行在5 FPS。

## 运行自定义模型


