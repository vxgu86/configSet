# 1 分析对比
**callbacks**与DRLDBackEnd完全一样，

**AirSimClient**与最新版本基本一致，多出来的几个函数挺有意思，

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

envs下也有较多地方不一致，其中有不少他自己的内容。

# 2 以下错误解决不了，
File "D:\Anaconda3\lib\site-packages\keras\engine\training_utils.py", line 128, in standardize_input_data
'with shape ' + str(data_shape))

ValueError: Error when checking input: expected input_1 to have 4 dimensions, but got array with shape (1, 1, 90, 256, 3)

/////////////////////////////////////////////////////////////////////////
in getScreenSceneVis()
img1d = np.array(bytearray(responses[0].image_data_uint8))#.reshape(responses[0].height, responses[0].width, 4)
if len(img1d) != (1442564): ----->should this be 1442563?

# 决定 20190731 先参照这个把DRLDBackEnd改到airsim新版本中进行研究。
