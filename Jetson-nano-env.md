# Jetson nano使用
## 概述
https://files.pythonhosted.org/packages/cb/97/361c8c6ceb3eb765371a702ea873ff2fe112fa40073e7d2b8199db8eb56e/scipy-1.3.0.tar.gz
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

安装Python包管理器 pip,
``` bash
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python3 get-pip.py
$ rm get-pip.py
``` 
**注意**
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

注意一定要在workon后安装，我在安装tf时没有进入workon，都安装到了
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
$ pip install scipy
$ pip install keras
```

安装耗时约35分钟。

## 安装Jetson推理引擎
与Jetson tx2不同的是，Jetson Nano .img已经安装了JetPack，而tx2装好后只是一个纯净版的Ubuntu。

因此这里可以直接构建Jetson推理引擎，参见[编译Jetson-inference代码](https://github.com/vxgu86/jetson-inference/blob/master/docs/%E7%BC%96%E8%AF%91Jetson-inference%E4%BB%A3%E7%A0%81.md) 。

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


