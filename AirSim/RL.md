# 20190729

## AirGym-master 老版本airsim

Airsim_RL-master新版本，可以跑，而且也是keras，只不过不是keras-rl

openai_drone_gym-master应该也是新版本，没跑过

### AirGym-master
先调用 根目录下的FileLogger的on_episode_end，后调用lib中rl callbacks.py中的TrainEpisodeLogger的on_episode_end

所以不必要纠结是否更新lib中rl callbacks.py中不同的FileLogger ，只会调用根目录下的。

目前lib中rl callbacks.py仍是修改过的，保留断点，看是否会有发现。


## AirGym-master适应性改进

self.goal = [0.0, 25.0] # global xy coordinates
myAirSimClient
-6---  -2  3个

将之调整到新版本的Airsim后，主要对env下的两个文件进行了更改。

改动后频发以下错误，这个问题主要是在take_action之后，怀疑有可能是新版本中 **什么时候加join**的问题。
``` bash
  File "D:/AirSim/PythonClient/multirotor/DQN-Train.py", line 96, in <module>
    dqn.fit(env, callbacks=callbacks, nb_steps=251000, visualize=False, verbose=2, log_interval=100)

  File "D:\Anaconda3\lib\site-packages\rl\core.py", line 177, in fit
    observation, r, done, info = env.step(action)

  File "D:\AirSim\PythonClient\multirotor\gym_airsim\envs\AirGym.py", line 119, in _step
    self.state = airgym.getScreenDepthVis(track)

  File "D:\AirSim\PythonClient\multirotor\gym_airsim\envs\myAirSimClient.py", line 135, in getScreenDepthVis
    img2d = np.reshape(img1d, (responses[0].height, responses[0].width))

  File "D:\Anaconda3\lib\site-packages\numpy\core\fromnumeric.py", line 292, in reshape
    return _wrapfunc(a, 'reshape', newshape, order=order)

  File "D:\Anaconda3\lib\site-packages\numpy\core\fromnumeric.py", line 56, in _wrapfunc
    return getattr(obj, method)(*args, **kwds)

ValueError: cannot reshape array of size 1 into shape (0,0)
``` 

openai_drone_gym-master在takeaction reset中都加了，其他地方都没加，straight函数也都没加，这样有意义吗？会不会straight还没结束就执行了takeaction中的?

先跑之间的AirGym-master在老环境中仿真，
``` bash
        collided = airgym.take_action(action)
        
        print("\n================in AirGym==_step==_take_action")
        time.sleep(5)
```
发现基本都是drone停下来后才打印输出，说明之前版本都是等价于加了join的,在takeaction reset中都加join后再测试。

确实不再出现该问题，说明之前是因为飞机没停稳就调用getimage是有问题的。

### 引入的新问题是，撞墙后还有动作，这是哪里的问题

明天现场调试，有可能是电脑久未关机


### 改动的值加入输出，进行对比，加深认识



### 是不是使用预训练过的模型




ppo 都改了什么






