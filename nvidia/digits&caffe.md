不管怎么设置，nvcaffe的cmake总是找到opencv2.4.9,而不是opencv3


安装protobuf-nvcaffe-digits

# 官方介绍安装protobuf-nvcaffe-digits
protobuf版本有影响
///////////////////////////////////////////////////////////
## nvcaffe在
1  opencv2.4.9 **后来发现这个是可以改的，CMakeCache.txt  但是undefined reference 问题仍在，需要重新编译opencv了**
2  etc/profile中  打开anaconda2
3  Makefile.config中用anaconda2，开启opencv3 相应opencv3的目录
情况下，此时cmake..确认python库为anaconda2，不能make通过，

tools/CMakeFiles/upgrade_solver_proto_text.dir/build.make:134: recipe for target 'tools/upgrade_solver_proto_text' failed
make[2]: *** [tools/upgrade_solver_proto_text] Error 1
CMakeFiles/Makefile2:701: recipe for target 'tools/CMakeFiles/upgrade_solver_proto_text.dir/all' failed
make[1]: *** [tools/CMakeFiles/upgrade_solver_proto_text.dir/all] Error 2
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFReadRGBAStrip@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFIsTiled@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFWriteScanline@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFGetField@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFScanlineSize@LIBTIFF_4.0'
//usr/lib/x86_64-linux-gnu/libSM.so.6: undefined reference to `uuid_generate@UUID_1.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFReadEncodedTile@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFReadRGBATile@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFClose@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFRGBAImageOK@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFOpen@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFReadEncodedStrip@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFSetField@LIBTIFF_4.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFSetWarningHandler@LIBTIFF_4.0'
//usr/lib/x86_64-linux-gnu/libSM.so.6: undefined reference to `uuid_unparse_lower@UUID_1.0'
/usr/lib/x86_64-linux-gnu/libopencv_highgui.so.2.4.9: undefined reference to `TIFFSetErrorHandler@LIBTIFF_4.0'

## nvcaffe在
1  opencv2.4.9
2  etc/profile中  关闭anaconda2
3  Makefile.config中用系统python，关掉opencv3 相应opencv3的目录
情况下，cmake。。确认库为/usr/bin/python,能make通过。
编译digits6.0.0报错，跑不起来。
编译digits6.0.0-rc.1错，跑不起来。
编译digits6.1.1通过，训练跑起来报错。


Setting up coverage_loss
Top shape: (1)
with loss weight 1
Memory required for data: 6129217288
Creating layer cluster





cmake后再想改环境需要clean下，有产生的中间文件了。
先要找教程
https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildProtobuf.md
https://github.com/NVIDIA/DIGITS/blob/master/docs/BuildCaffe.md

DetectNet, NVcaffe version 0.15.1 or later is required,否则不会有detectnet之类的库
Message type "caffe.LayerParameter" has no field named "detectnet_groundtruth_param"
