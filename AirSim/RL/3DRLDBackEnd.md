# 1 对比
AirSimClient 与airgym完全一致，

callbacks增加了记录当下最好weights功能

其他变化都较大

# 2 直接在旧版本中运行时，一直转来转去，猜测是因为上个动作没做完，就开始执行了下个动作。

20190801

1修改  在move中sleep 看是否会向前飞，

            self.moveByVelocity(0, 0, 0, 1)
            self.rotateByYawRate(0, 1)
忘记是什么样子了，直接在新版本中改好了。

2搞明白下面的东西，方向和飞行的问题。
https://github.com/microsoft/AirSim/issues/688
https://github.com/microsoft/AirSim/issues/985

3参考Drone改为新版本。

已经跑起来了，改了一些东西。

现在一个问题，有没有探索空间这个问题，跟AirGym一样，左右rotate的角度是不一样的。要能作出任意想做的动作，
