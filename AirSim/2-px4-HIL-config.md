PX4软件栈是一个非常流行的开源的飞行控制器，支持各种电路板和传感器，以及对更高级别的任务，如任务规划等功能，具体可访问px4.io了解更多信息。

AirSim是一个基于虚幻引擎(Unreal Engine)的开源、跨平台无人机模拟器。
它可以使用硬件在环（HITL）或软件在环（SITL）的方式为Pixhawk / PX4提供逼真的物理和视觉仿真。

目的是在Airsim+Unreal（unity）中加入pixhawk硬件在环仿真（HIL）。
现在知道这个MarVlik的实现是在AirLib中，想办法弄明白。

AirSim中目前默认的是[simple flight](https://github.com/microsoft/AirSim/blob/master/docs/simple_flight.md）。

插入飞控，QGroundControl中刷最新的 PX4 Flight Stack，机架选择HIL Quadrocopter X airframe，确认并重启。

Radio 校准

Flight Mode 里选择一个remote control switches开关作为Mode Channel，然后设定这个开关的两个位置为Stabilized和 Attitude两个飞行模式。

Tuning这个界面就要看不同的飞控和遥控了。

最后就是[AirSim settings](settings.md)
```
{
  "SettingsVersion": 1.2,
  "SimMode": "Multirotor",
  "Vehicles": {
    "PX4": {
      "VehicleType": "PX4Multirotor"
    }
  }
}
```
