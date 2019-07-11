
按教程编译结束之后并无错误，在unity中打开demo时一直提示，
Problem in starting AirSim Server!!!
Please check logs for information.
而logs中则没有东西，因为server都没启动起来。


截图

这时settings.json如下：

```
{
    "SettingsVersion": 1.2,
    "SeeDocsAt": "https://github.com/Microsoft/AirSim/blob/master/docs/settings.md",
    "SimMode": "Multirotor",
    "Vehicles": {
        "PX4": {
          "VehicleType": "PX4Multirotor"
        }
      }
}

```

不知道从哪里下手，只好翻issues，终于找到。
AirSim/Unity/UnityDemo/Assets/AirSimAssets/Scripts/Utilities/AirSimSettings.cs无法像Unreal那样读取多样化的配置项，就包括读取“Vehicles”这个配置项，这其实是一个限制性很大的问题，那么依赖于这个选项的所有功能都被堵住了，其中就包括多agents。

尝试
1 去掉    

```
      "Vehicles": {
        "PX4": {
          "VehicleType": "PX4Multirotor"
        }
      }
      
```
 整个去掉不行，没有默认，也不能不存在。
 2 "DefaultVehicleConfig": "PX4", 也不行，因为这个工具的配置没有编译 SITL 或者 HIL。
 
 drone和car通过的如下：
```
{
  "SeeDocsAt": "https://github.com/Microsoft/AirSim/blob/master/docs/settings.md",
  "SettingsVersion": 1.2,
    "SimMode": "Multirotor",
	"DefaultVehicleConfig": "SimpleFlight",
  "Vehicles": {
    "SimpleFlight": {
      "VehicleType": "SimpleFlight"
    }
  }
}
-------------------------------------------------------------------------------------------
{
  "SeeDocsAt": "https://github.com/Microsoft/AirSim/blob/master/docs/settings.md",
  "SettingsVersion": 1.2,
    "SimMode": "Car",
	"DefaultVehicleConfig": "PhysXCar",
  "Vehicles": {
    "PhysXCar": {
      "VehicleType": "PhysXCar"
    }
  }
}

```

