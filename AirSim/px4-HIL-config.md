AirSim是一个基于虚幻引擎(Unreal Engine)的开源、跨平台无人机模拟器。
它可以使用硬件在环（HITL）或软件在环（SITL）的方式为Pixhawk / PX4提供逼真的物理和视觉仿真。

目的是在Airsim+Unreal（unity）中加入pixhawk硬件在环仿真（HIL）。
现在知道这个MarVlik的实现是在AirLib中，想办法弄明白。

AirSim中目前默认的是[simple flight](https://github.com/microsoft/AirSim/blob/master/docs/simple_flight.md）。

QGroundControl中刷最新的 PX4 Flight Stack，
