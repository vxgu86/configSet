# python的使用

python hello_car.py 
python hello_drone

examples 怎么跑起来

c++  DroneShell

HelloDrone
HelloCar


## failsafe的解除

arm--takeoff

param set COM_OBL_ACT 1      原来是land 

param set COM_OBL_RC_ACT 5   原来是position

改这些都没用，有一个时间指标，从0改为5s，ok。，网址找到后放上来。

https://github.com/microsoft/AirSim/issues?utf8=%E2%9C%93&q=droneshell+land

https://github.com/microsoft/AirSim/issues/393

http://px4-travis.s3.amazonaws.com/Firmware/stable/px4fmu-v3_default.px4   
