# Jetson nano使用
## 概述

/usr/local/cuda-10.0 是系统自带的。

swap???

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
**python3是不是系统自带的？在pip python3-dev之前试试。**
which python
python --version
which python3
python3 --version

看到python3 get-pip.py才意识到，可能是which python3 
``` bash
vxgunano@vx-heaven:~$ which python
/usr/bin/python
vxgunano@vx-heaven:~$ python --version
Python 2.7.15rc1
vxgunano@vx-heaven:~/cvexp$ which python3
/usr/bin/python3
vxgunano@vx-heaven:~/cvexp$ python3 --version
Python 3.6.8
```

## 配置Python开发环境

安装Python包管理器 pip,
``` bash
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python3 get-pip.py
$ rm get-pip.py
``` 

使用Python virtual environments可保持多个Python开发环境相互独立，便于在一张SD卡上维护不同的开发环境 。
这是一个好习惯，使环境之间互不干扰。比如一个Python + OpenCV 的项目需要scikit-learn (v0.14)，但其他的有需要新版本的scikit-learn (0.19)。
虚拟环境有很多种，virtualenv+virtualenvwrapper是一种，也可以用conda或者PyEnv。

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
the belowing shows
``` bash
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/premkproject
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postmkproject
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/initialize
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/premkvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postmkvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/prermvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postrmvirtualenv
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/predeactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postdeactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/preactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/postactivate
virtualenvwrapper.user_scripts creating /home/vxnano/.virtualenvs/get_env_details
``` 

现在可以使用mkvirtualenv命令创建一个Python虚拟环境，命名虚拟环境为cvnano。
``` bash
$ mkvirtualenv cvnano -p python3
``` 
另外，名字起的最好有区别性如
py3cv4
py3cv3
py2cv2

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
``` bash
  WARNING: Building wheel for termcolor failed: [Errno 13] Permission denied: '/home/vxnano/.cache/pip/wheels/7c'
  WARNING: Building wheel for grpcio failed: [Errno 13] Permission denied: '/home/vxnano/.cache/pip/wheels/c2'
  WARNING: Building wheel for gast failed: [Errno 13] Permission denied: '/home/vxnano/.cache/pip/wheels/5c'
  WARNING: Building wheel for absl-py failed: [Errno 13] Permission denied: '/home/vxnano/.cache/pip/wheels/ee'
  WARNING: Building wheel for h5py failed: [Errno 13] Permission denied: '/home/vxnano/.cache/pip/wheels/0a'
``` 

这里有个问题，不管是不是workon，tf都装在系统上，而不是虚拟环境中。
``` bash
Looking in indexes: https://pypi.org/simple, https://developer.download.nvidia.com/compute/redist/jp/v42
Requirement already satisfied: tensorflow-gpu==1.13.1+nv19.3 in /usr/local/lib/python3.6/dist-packages (1.13.1+nv19.3)
Requirement already satisfied: termcolor>=1.1.0 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.1.0)
Requirement already satisfied: grpcio>=1.8.6 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.21.1)
Requirement already satisfied: six>=1.10.0 in /usr/lib/python3/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.11.0)
Requirement already satisfied: keras-preprocessing>=1.0.5 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.1.0)
Requirement already satisfied: tensorflow-estimator<1.14.0rc0,>=1.13.0 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.13.0)
Requirement already satisfied: keras-applications>=1.0.6 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.0.8)
Requirement already satisfied: protobuf>=3.6.1 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (3.8.0)
Requirement already satisfied: absl-py>=0.1.6 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (0.7.1)
Requirement already satisfied: tensorboard<1.14.0,>=1.13.0 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.13.1)
Requirement already satisfied: wheel>=0.26 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (0.33.4)
Requirement already satisfied: numpy>=1.13.3 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (1.16.4)
Requirement already satisfied: astor>=0.6.0 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (0.8.0)
Requirement already satisfied: gast>=0.2.0 in /usr/local/lib/python3.6/dist-packages (from tensorflow-gpu==1.13.1+nv19.3) (0.2.2)
Requirement already satisfied: mock>=2.0.0 in /usr/local/lib/python3.6/dist-packages (from tensorflow-estimator<1.14.0rc0,>=1.13.0->tensorflow-gpu==1.13.1+nv19.3) (3.0.5)
Requirement already satisfied: h5py in /usr/local/lib/python3.6/dist-packages (from keras-applications>=1.0.6->tensorflow-gpu==1.13.1+nv19.3) (2.9.0)
Requirement already satisfied: setuptools in /usr/local/lib/python3.6/dist-packages (from protobuf>=3.6.1->tensorflow-gpu==1.13.1+nv19.3) (41.0.1)
Requirement already satisfied: werkzeug>=0.11.15 in /usr/local/lib/python3.6/dist-packages (from tensorboard<1.14.0,>=1.13.0->tensorflow-gpu==1.13.1+nv19.3) (0.15.4)
Requirement already satisfied: markdown>=2.6.8 in /usr/local/lib/python3.6/dist-packages (from tensorboard<1.14.0,>=1.13.0->tensorflow-gpu==1.13.1+nv19.3) (3.1.1)
``` 

最后一步是安装SciPy和Keras：

``` bash
$ sudo pip install scipy
$ sudo pip install keras
```

安装耗时约35分钟。

## 安装opencv
opencv的安装也是必须的，这是一个非常有用的计算机视觉开发包。
因为opencv 的安装比较通用，可参考这里。

## 安装Jetson推理引擎
与Jetson tx2不同的是，Jetson Nano .img已经安装了JetPack，而tx2装好后只是一个纯净版的Ubuntu。

因此这里可以直接构建Jetson推理引擎，参见[编译Jetson-inference代码](https://github.com/vxgu86/jetson-inference/blob/master/docs/%E7%BC%96%E8%AF%91Jetson-inference%E4%BB%A3%E7%A0%81.md) 。

## 外接camera设置

NVIDIA Jetson Nano时有两种输入摄像头设备选项：

-- CSI相机模块，如Raspberry Pi camera模块
-- USB网络摄像头

这里以Logitech C920为例，可以在Nano上即插即用。

在以camera为输入的例子中，DEFAULT_CAMERA值设置为 -1，这表示使用的是CSI摄像头。如果使用USB摄像头，需要改变 DEFAULT_CAMERA为0（或任何正确的/dev/video V4L2摄像头）。

**ls /dev | grep video 我这里显示有时是video1，有时是video0**

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

如果库编译时启用了GPU支持，相应的代码在GPU类设备上推理inference时就会自动运行在GPU上。如安装的tensorflow和keras，相应的代码运行时就会自动在GPU上运行；利用二者预训练的模型也会自动GPU执行运算。

在Digits中训练的模型，可直接在命令行调用。

如果Jetson nano支持Keras, TensorFlow, Caffe, Torch/PyTorch等深度学习库，就可以将相应的代码跑在上面。

但是，OpenCV的深度神经网络模块却并不支持NVIDIA GPU，当然也包括Jetson nano。在正式支持之前，我们无法使cv2.dnn函数在GPU上运行。
不过，Intel的OpenVINO toolkit, Movidius NCS, 以及其他OpenVINO兼容系列的产品都已经支持OpenCV的深度神经网络模块。


