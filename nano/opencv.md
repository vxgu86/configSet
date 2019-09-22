# 1 pip: command not found

wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py
pip -V　　#查看pip版本

# 2 'module' object has no attribute 'xfeatures2d'

pip install opencv-contrib-python
install 4.0


opencv-python\opencv_contrib\modules\xfeatures2d\src\sift.cpp:1207: error: (-213:The function/feature is not implemented) This algorithm is patented and is excluded in this configuration; Set OPENCV_ENABLE_NONFREE CMake option and rebuild the library in function ‘cv::xfeatures2d::SIFT::create’
貌似是该算法被申请了专利，将opencv版本退到3.4.2即可解决，卸载之前的包，然后
pip install opencv-python == 3.4.2.16

# 3 Unable to locate package libjasper-dev
在ubuntu18.04系统上安装opencv但是在安装依赖包的过程中，有一个依赖包，libjasper-dev在使用命令

    sudo apt-get install libjaster-dev

提示：errorE: unable to locate libjasper-dev

sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"
sudo apt update
sudo apt install libjasper1 libjasper-dev

成功的解决了问题，其中libjasper1是libjasper-dev的依赖包


different aarm64

