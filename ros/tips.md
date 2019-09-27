# 1 CMake Error at zed-ros-wrapper/zed_wrapper/CMakeLists.txt:156 (roslint_cpp):
  Unknown CMake command "roslint_cpp".

install the missing dependency with the command
sudo apt-get install ros-kinetic-roslint


# 2 install
To install all the dependency required you can go to the root of your catkin workspace and run this command:
$ rosdep install --from-paths src --ignore-src -r -y

Here you can find the documentation about the rosdep command:
http://wiki.ros.org/rosdep
