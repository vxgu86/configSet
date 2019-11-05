pkg-config opencv --modversion  随着/etc/profile的source会变动
但caffe的cmake时opencv库一直是2.4.9.1，找不到

# 官方介绍安装protobuf-nvcaffe-digits
protobuf版本有影响
///////////////////////////////////////////////////////////
nvcaffe在
1  opencv2.4.9
2  etc/profile中  打开anaconda2
3  Makefile.config中用anaconda2，开启opencv3 相应opencv3的目录
情况下，此时cmake..确认python库为anaconda2，不能make通过，
undefined reference to ‘’

nvcaffe在
1  opencv2.4.9
2  etc/profile中  关闭anaconda2
3  Makefile.config中用系统python，关掉opencv3 相应opencv3的目录
情况下，cmake。。确认库为/usr/bin/python,能make通过。
编译digits6.0.0报错，跑不起来。
编译digits6.1.1通过，训练跑起来报错。









cmake后再想改环境需要clean下，有产生的中间文件了。
先要找教程
https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildProtobuf.md
https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildCaffe.md

DetectNet, NVcaffe version 0.15.1 or later is required,否则不会有detectnet之类的库
Message type "caffe.LayerParameter" has no field named "detectnet_groundtruth_param"
