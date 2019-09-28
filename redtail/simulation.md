uname -r system kernel version

# 1 docker 
https://docs.docker.com/install/linux/docker-ce/ubuntu/   install from package 

# 2 nvidia-docker
https://nvidia.github.io/nvidia-docker/
```
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update
```
```
vxgu@vxgu-SVS15128CCB:~/jetpackafter$ sudo apt-get install nvidia-docker
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  bridge-utils containerd runc ubuntu-fan
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  nvidia-docker
0 upgraded, 1 newly installed, 0 to remove and 262 not upgraded.
Need to get 2,266 kB of archives.
After this operation, 14.1 MB of additional disk space will be used.
Get:1 https://nvidia.github.io/nvidia-docker/ubuntu16.04/amd64  nvidia-docker 1.0.1-1 [2,266 kB]
Fetched 2,266 kB in 3s (672 kB/s)        
Selecting previously unselected package nvidia-docker.
(Reading database ... 211893 files and directories currently installed.)
Preparing to unpack .../nvidia-docker_1.0.1-1_amd64.deb ...
Unpacking nvidia-docker (1.0.1-1) ...
Processing triggers for ureadahead (0.100.0-19) ...
Setting up nvidia-docker (1.0.1-1) ...
Configuring user
Setting up permissions
Job for nvidia-docker.service failed because the control process exited with error code. See "systemctl status nvidia-docker.service" and "journalctl -xe" for details.
nvidia-docker.service couldn't start.
Processing triggers for ureadahead (0.100.0-19) ...
```
**already installed,could not started**

vxgu@vxgu-SVS15128CCB:~/jetpackafter$ systemctl status nvidia-docker.service
● nvidia-docker.service - NVIDIA Docker plugin
   Loaded: loaded (/lib/systemd/system/nvidia-docker.service; enabled; vendor preset: enabled)
   Active: failed (Result: start-limit-hit) since 四 2019-09-26 00:26:54 CST; 3min 35s ago
     Docs: https://github.com/NVIDIA/nvidia-docker/wiki
  Process: 9738 ExecStopPost=/bin/rm -f $SPEC_FILE (code=exited, status=0/SUCCESS)
  Process: 9734 ExecStartPost=/bin/sh -c /bin/echo unix://$SOCK_DIR/nvidia-docker.sock > $SPEC_FILE (code=exited, status=0/SUCCESS)
  Process: 9720 ExecStartPost=/bin/sh -c /bin/mkdir -p $( dirname $SPEC_FILE ) (code=exited, status=0/SUCCESS)
  Process: 9719 ExecStart=/usr/bin/nvidia-docker-plugin -s $SOCK_DIR (code=exited, status=1/FAILURE)
 Main PID: 9719 (code=exited, status=1/FAILURE)

9月 26 00:26:53 vxgu-SVS15128CCB systemd[1]: Failed to start NVIDIA Docker plugin.
9月 26 00:26:53 vxgu-SVS15128CCB systemd[1]: nvidia-docker.service: Unit entered failed state.
9月 26 00:26:53 vxgu-SVS15128CCB systemd[1]: nvidia-docker.service: Failed with result 'exit-code'.
9月 26 00:26:54 vxgu-SVS15128CCB systemd[1]: nvidia-docker.service: Service hold-off time over, scheduling restart.
9月 26 00:26:54 vxgu-SVS15128CCB systemd[1]: Stopped NVIDIA Docker plugin.
9月 26 00:26:54 vxgu-SVS15128CCB systemd[1]: nvidia-docker.service: Start request repeated too quickly.
9月 26 00:26:54 vxgu-SVS15128CCB systemd[1]: Failed to start NVIDIA Docker plugin.
9月 26 00:26:54 vxgu-SVS15128CCB systemd[1]: nvidia-docker.service: Unit entered failed state.
9月 26 00:26:54 vxgu-SVS15128CCB systemd[1]: nvidia-docker.service: Failed with result 'start-limit-hit'.

request of nvidia-docker
 NVIDIA drivers >= 340.29 with binary nvidia-modprobe 
 
sudo apt install nvidia-modprobe
sudo systemctl start nvidia-docker
sudo systemctl status nvidia-docker



