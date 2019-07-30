# 20190729

## AirGym-master 老版本airsim，改为新版本后一直有问题。

openai_drone_gym-master是改的AirGym-master，应该是新版本，没跑过

DRLDBackEnd是AirGym的升级版，有升级，也是用的老版本airsim，用老版本的blocks环境能跑。

DroneTracking改的DRLDBackEnd，新版本

**callbacks**完全一样，**AirSimClient**与最新版本基本一致，多出来的几个函数挺有意思，

    def showPlannedWaypoints(self, x1, y1, z1, x2, y2, z2, thickness=50, lifetime=10, debug_line_color='red', vehicle_name = ''):
        self.client.call('simShowPlannedWaypoints', x1, y1, z1, x2, y2, z2, thickness, lifetime, debug_line_color, vehicle_name)
        
    def simShowDebugLines(self, x1, y1, z1, x2, y2, z2, thickness=50, lifetime=10, debug_line_color='red'):
        self.client.call('simShowDebugLines', x1, y1, z1, x2, y2, z2, thickness, lifetime, debug_line_color)
        
    def simShowPawnPath(self, showPath:'bool', debug_line_lifetime, debug_line_thickness, vehicle_name = ''):
        self.client.call('simShowPawnPath', showPath, debug_line_lifetime, debug_line_thickness, vehicle_name)
        下面几个也没有
    # query vehicle state
    def getPitchRollYaw(self, vehicle_name = ''):
        return self.toEulerianAngle(self.simGetGroundTruthKinematics(vehicle_name).orientation)

    def timestampNow(self):
        return self.client.call('timestampNow')
 
    def isSimulationMode(self):
        return self.client.call('isSimulationMode')
    def getServerDebugInfo(self):
        return self.client.call('getServerDebugInfo')
        
DQN-Train   不一样的地方还不少。



envs下未看



Airsim_RL-master PPO，新版本的Airsim，可以跑，而且也是keras，只不过不是keras-rl，跑的一直不出结果，也不见有改进。





ppo 都改了什么






