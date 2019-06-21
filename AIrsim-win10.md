对于 Unreal Engine 来说，AirSim 其实是作为一个插件存在，是把无人车，无人机以插件的形式加入 Unreal 的场景中。

目前的版本要求为：
Epic Games Launcher--Unreal Engine 4.18（注意在下面的安装之前将current设置为这个版本）  
Visual Studio 2017（VC++ / Windows SDK 8.1两个包要安装）

**编译Airsim**
（1）克隆下来: git clone https://github.com/Microsoft/AirSim.git, 

（2）打开 x64 Native Tools Command Prompt for VS 2017。cd AirSim，build.cmd，执行后会在Unreal\Plugins直接创建plugin，使用时拷入Unreal项目即可。
执行时会有一个bug，
d:\airsim\airlib\deps\eigen3\eigen\src\core\arch\cuda\half.h : error C2220: 警告被视为错误 - 没有生成“object”文件 [D:\AirSim\AirLib\A
irLib.vcxproj]
d:\airsim\airlib\deps\eigen3\eigen\src\core\arch\cuda\half.h : warning C4819: 该文件包含不能在当前代码页(936)中表示的字符。请将该文件保存为 Unicode
格式以防止数据丢失 [D:\AirSim\AirLib\AirLib.vcxproj]
  RpcLibServerBase.cpp
。。。
  MultirotorApiBase.cpp
。。。
。。。

  
**构建Unreal 项目**

