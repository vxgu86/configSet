# 1、概述

## AirGym-master 

老版本airsim，改为新版本后一直有问题, responses = self.simGetImages经常为0，不改了，原理已经验证。

## openai_drone_gym-master

改的AirGym-master，应该是新版本，没跑过。

## DRLDBackEnd

AirGym的升级版，用的老版本airsim，用老版本的blocks环境能跑，存在问题。

## DroneTracking

改的DRLDBackEnd，新版本，我对images的理解有问题，待进一步理解后研究。
该作者还有其他资料。





Airsim_RL-master PPO，新版本的Airsim，可以跑，而且也是keras，只不过不是keras-rl，跑的一直不出结果，也不见有改进。

ppo 都改了什么


# 2、训练记录

直接在复杂环境中训练，相当于让一个婴儿直接学泛函，应该首先降低环境复杂度，或者将目标分解，逐个通过加载模型的方式进行训练。

在室内避障时，先去掉室内所有障碍，训练目标方向，然后加上室内障碍，但是同高度，训练避障，然后调整窗户高度，训练高低维度。

20190814

模型能够停下来了，而不是一直滑行；

但在起飞区域一直徘徊，甚至飞进窗户后又飞出来。这是不是因为奖励中我设置的时间系数低了，因为距离比AirGym要近所以设为1---0.1了，改为0.8尝试。



