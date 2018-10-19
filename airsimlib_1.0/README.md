
# Airsim lib v1.0

主要功能： 将airsim Lib封装成一个小型的动态库，便于集成和使用

## 首先设置airsim 的根目录，以及airsim所依赖的 rcp库

```
## set source path
set(AIRSIM_ROOT "/home/hualong/ssd/software/AirSim_ROS")
set(RPC_Lib "${AIRSIM_ROOT}/external/rpclib/rpclib-2.2.1")
```

## 然后编译产生 AirLib库

> cmake .
> make
