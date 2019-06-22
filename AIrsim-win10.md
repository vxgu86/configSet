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

（1）以Landscape Mountain为例，到下载目录中打开LandscapeMountains.uproject，
File菜单-- New C++ class默认类的类型None 和名字MyClass, 点击Create Class。Unreal要求项目中至少有一个source file，触发编译后会打开相应的LandscapeMountains.sln。

（2）**从AirSim拷贝Unreal\Plugins到LandscapeMountains文件夹。**

（3）然后打开并修改LandscapeMountains.uproject
``` bash
{
    "FileVersion": 3,
    "EngineAssociation": "4.18",
    "Category": "Samples",
    "Description": "",
    "Modules": [
        {
            "Name": "LandscapeMountains",
            "Type": "Runtime",
            "LoadingPhase": "Default",   
            "AdditionalDependencies": [
                "AirSim"
            ]
        }
    ],
    "TargetPlatforms": [
        "MacNoEditor",
        "WindowsNoEditor"
    ],
    "Plugins": [
        {
            "Name": "AirSim",
            "Enabled": true
        }
    ]
}
```
**注意** 如果是组内最后一项，不用“，”，但是后面还有内容的话就要加“，”，否则会报错。
Couldn't set association for project. Check the file is writeable

（4）关闭Visual Studio 和Unreal Editor，在**LandscapeMountains.uproject**右击并选择**Generate Visual Studio Project Files**。
生成结束后重新打开LandscapeMountains.sln，设置生成选项为DebugGame Editor Win64，F5运行后会打开Unreal Editor，这时候就可以修改environment, assets等游戏资源。
（5）在这个环境中首先要做的事情是添加PlayerStart对象，在世界大纲视图（World Outliner）中，注意location 不要太高，这是AirSim plugin创建
vehicle的位置。

然后在窗口Window-世界设置World Settings里设置GameMode Override为AirSimGameMode。

（6）'Edit->Editor Preferences' ，搜索框中搜'CPU'，将'Use Less CPU when in Background'去掉勾选，这样UE失去焦点后也不会降速的太厉害。

保存后就可以运行，配置结束。

**选择仿真器**

设置仿真汽车还是无人机，可参见[SimMode](settings.md#SimMode)，也可以看[car设置](using_car.md)。

**保持项目环境中AirSim与Github中版本一致**

保持AirSim的代码与Github中的一致，需要经常从Github将本地Airsim代码更新为最新版本。

1 将clean.bat（linux用户为 clean.sh）放在环境的根文件夹，运行此文件以清除Unreal项目中生成的中间文件；

2 git pull下repo，然后build.cmd（Linux用户为 /build.sh）；

3 再将airsim/unreal/plugins文件夹拷入 项目/plugins文件夹来替换。

4 右键单击.uproject文件并选择“Generate Visual Studio Project Files”。Linux不需要这样做。

