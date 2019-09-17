

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
		     
```
带有, False, False的话，程序会卡住。

直接去掉后，得到的会是RGBA，直接放入DIGITS中作为数据集会提示错误，进行RGBA-RGB转换后使用。
``` bash
responses = client.simGetImages([
    airsim.ImageRequest("3", airsim.ImageType.Scene),
    airsim.ImageRequest("3", airsim.ImageType.Segmentation)]) 	     
```
取 0 0 镜头的可以，0 3镜头也可，3 3 就一直卡在第二个request处。 找了半天不知道哪里出问题，后来看到Blocks项目的配置为development editor，改了之后居然好了。。。。



