# 1 18.04LTS 换源
$ sudo vim /etc/apt/sources.list


# 阿里源
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

# 阿里源
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse


$ sudo apt update && sudo apt upgrade

# 清华源
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse


port de wenti, which pc did it?


Reading package lists... Done
E: Failed to fetch http://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/xenial/main/binary-arm64/Packages  404  Not Found [IP: 101.6.8.193 80]
E: Failed to fetch http://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/xenial-updates/main/binary-arm64/Packages  404  Not Found [IP: 101.6.8.193 80]
E: Failed to fetch http://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/xenial-backports/main/binary-arm64/Packages  404  Not Found [IP: 101.6.8.193 80]
E: Failed to fetch http://mirrors.tuna.tsinghua.edu.cn/ubuntu/dists/xenial-security/main/binary-arm64/Packages  404  Not Found [IP: 101.6.8.193 80]
E: Some index files failed to download. They have been ignored, or old ones used instead.


dpkg --print-foreign-architectures
i386
arm64

vxgu@vxgu-SVS15128CCB:/etc/resolvconf/resolv.conf.d$ sudo apt-get install gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package gstreamer1.0-plugins-bad
E: Couldn't find any package by glob 'gstreamer1.0-plugins-bad'
E: Couldn't find any package by regex 'gstreamer1.0-plugins-bad'
E: Unable to locate package gstreamer1.0-plugins-ugly
E: Couldn't find any package by glob 'gstreamer1.0-plugins-ugly'
E: Couldn't find any package by regex 'gstreamer1.0-plugins-ugly'
vxgu@vxgu-SVS15128CCB:/etc/resolvconf/resolv.conf.d$ 
vxgu@vxgu-SVS15128CCB:/etc/resolvconf/resolv.conf.d$ sudo apt-get install libgstreamer1.0-0
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package libgstreamer1.0-0 is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'libgstreamer1.0-0' has no installation candidate



