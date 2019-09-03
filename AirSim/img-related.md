

``` bash
ImageRequest(const std::string& camera_name_val, ImageCaptureBase::ImageType image_type_val, 
             bool pixels_as_float_val = false, bool compress_val = true)
        {
            camera_name = camera_name_val;
            image_type = image_type_val;
            pixels_as_float = pixels_as_float_val;
            compress = compress_val;
        }

    responses = client.simGetImages([
        airsim.ImageRequest("0", airsim.ImageType.Segmentation, False, False)])  #scene vision image in uncompressed RGBA array
带有, False, False的话，程序会卡住。
直接去掉后，得到的会是RGBA，直接放入DIGITS中作为数据集会提示错误。

        
moveByVelocityAsync(float vx, float vy, float vz, float duration, 
                   DrivetrainType drivetrain, const YawMode& yaw_mode, const std::string& vehicle_name)
		     
```


强化学习中，env reward已定，调整寻优policy

**改动

1 simpleflight做仿真

2 tf1.14.0版本一直提示模型restore错误，起先将resume=False，显式设置为false后不提示。但我训练的一直不好用，想试一下原作训练的。
后将tf恢复至1.13版本后无提示。
``` bash
Key 。。。。。 not found in checkpoint
	 [[node save/RestoreV2 (defined at 。。。。。
```

3 我的环境大小与code中的不同，更改了
``` bash
goalY = 25
goals = [2, 5.2, 8.4, 11.6, 14.8,21.2,25]
``` 
4 playerstart在z方向很大，无人机导入后上下的空间也会存在，因为试验时发现，在上方3m处放置collision板，在不到3m处就开始提示，应该是player的空间，虽然看不见，压缩至-0.25，调整一下后无人机差不多能飞到将近3m。

5 无人机过宽，比赛要求轴距80，换算的话宽度480即可改playerstart的x-y无反应，在BP_FlyingPawn中将xy方向的缩放直接改为0.5，无人机的长宽变为50cm。



先把这些算法都弄熟练，后面再引入双视融合
只有深度信息是不足以引导无人机出来的，需要加入egmentation。
