
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




## 复制 include依赖头文件

- 进入到Airsim/AirLib/include
- 将include下的文件夹复制到 airsimlib_1.0/include下



## 使用 airsimlib_1.0

在CmakeLists.txt文件中
```
set(AIRLIB_ROOT "/home/hualong/ssd/coding/uav_ros/src/redtail/airsimlib_1.0" )
include_directories( ${AIRLIB_ROOT}/include/Airlib)
link_directories(${AIRSIM_ROOT}/x86_64/lib)

add_executable(***) or add_library()
target_link_libraries( *****

AirLib
)


```
