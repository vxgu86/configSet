Airsim是一个基于Unreal Engine（虚幻引擎4）的插件，这意味着Airsim单独是无法跑起来的。用来模拟无人机或无人车在真实环境下的控制，由微软发布在github平台。更多详细文字介绍与视频可以查看github主页。

对于 Unreal Engine 来说，AirSim 其实是作为一个插件存在，是把无人车，无人机以插件的形式加入 Unreal 的场景中。

目前的版本要求为：
Epic Games Launcher--**Unreal Engine 4.18**（注意在下面的安装之前将current设置为这个版本），可在  “虚拟引擎-学习”处找到“山脉景观” ，

**Visual Studio 2017**（VC++ / Windows SDK 8.1两个包要安装）


Airsim有已经编译好的直接下载版本，如ZhangJiaJie等，但是要开发还是得自己编译。

**编译Airsim**
（1）克隆下来: git clone https://github.com/Microsoft/AirSim.git, 

（2）打开 x64 Native Tools Command Prompt for VS 2017。cd AirSim，build.cmd，执行后会在Unreal\Plugins直接创建plugin，使用时拷入Unreal项目即可。

执行时会有一个bug，
``` bash
d:\airsim\airlib\deps\eigen3\eigen\src\core\arch\cuda\half.h : error C2220: 警告被视为错误 - 没有生成“object”文件 [D:\AirSim\AirLib\A
irLib.vcxproj]
d:\airsim\airlib\deps\eigen3\eigen\src\core\arch\cuda\half.h : warning C4819: 该文件包含不能在当前代码页(936)中表示的字符。请将该文件保存为 Unicode
格式以防止数据丢失 [D:\AirSim\AirLib\AirLib.vcxproj]
  RpcLibServerBase.cpp
。。。
  MultirotorApiBase.cpp
。。。
。。。
```
这个bug是因为half.h 在注释部分使用了非 UTF-8 编码的双引号导致的。找到这个文件，将 16 行的 "AS IS"的引号替换一下。

**体验已有Blocks 项目**

Blocks 是Airsim自带的一个项目，主要用来进行测试，基础，且执行速度很快。来到AirSim\Unreal\Environments\Blocks目录，双击update_from_git.bat。

双击生成的.sln 文件来打开Visual Studio 2017。

设置Blocks project为启动项目（深色），调试选项设置为 DebugGame_Editor / Win64，F5运行。

在打开的Unreal Engine中点击运行。

在Visual Studio中修改代码之后需要重新编译，点击 F5 重新运行。AirSim\Unreal\Environments\Blocks目录下还有几个batch文件来同步代码/清理等。

**新建Unreal+AirSim项目**
