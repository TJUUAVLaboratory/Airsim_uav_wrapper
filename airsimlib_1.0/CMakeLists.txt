cmake_minimum_required(VERSION 2.8)
project(AirLib)

##print output message
message("--system arch:   ${CMAKE_SYSTEM_PROCESSOR}")
message("--output path:   ${PROJECT_OUTPUT_DIR}")


##set output path

set(PROJECT_OUTPUT_DIR ${PROJECT_BINARY_DIR}/${CMAKE_SYSTEM_PROCESSOR})
SET(PROJECT_INCLUDE_DIR ${PROJECT_BINARY_DIR}/include/Airlib)
SET(PROJECT_SRC_DIR ${PROJECT_BINARY_DIR}/src)

# mkdir directory
file(MAKE_DIRECTORY ${PROJECT_INCLUDE_DIR}) 
file(MAKE_DIRECTORY ${PROJECT_SRC_DIR}) 
FILE(MAKE_DIRECTORY ${PROJECT_OUTPUT_DIR}/bin)
FILE(MAKE_DIRECTORY ${PROJECT_OUTPUT_DIR}/lib)

## set the target path
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_OUTPUT_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_OUTPUT_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_OUTPUT_DIR}/lib)


## set source path
set(AIRSIM_ROOT "/home/hualong/ssd/software/AirSim_ROS")
set(RPC_Lib "${AIRSIM_ROOT}/external/rpclib/rpclib-2.2.1")

message(STATUS "AIRSIM_ROOT: ${AIRSIM_ROOT}")
message(STATUS "RPC_Lib: ${RPC_Lib}")

## set c++11 编译选项
# -std=c++11 包含C++11特性
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")  

find_package(Eigen3 REQUIRED)
find_package(OpenCV REQUIRED)
find_package(PCL    REQUIRED)


## 头文件
include_directories(
    ${AIRSIM_ROOT}/AirLib/include
    ${RPC_Lib}/include
    ${EIGEN3_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
)

##头文件
file(GLOB airsim_include
${AIRSIM_ROOT}/AirLib/include/vehicles/multirotor/api/*.hpp
${AIRSIM_ROOT}/AirLib/include/api/*.hpp
${RPC_Lib}/include/rpc/*.h
${AIRSIM_ROOT}/AirLib/deps/MavLinkCom/include/*.hpp
)

# transfer all headers to the include directory
##message("copy the include file ")
##foreach(include ${airsim_include})
##	configure_file(${include} ${PROJECT_INCLUDE_DIR} COPYONLY)
##endforeach()



## 源文件
file(GLOB  airsim_source
${AIRSIM_ROOT}/AirLib/src/api/*cpp
${AIRSIM_ROOT}/AirLib/src/common/common_utils/*.cpp
${AIRSIM_ROOT}/AirLib/src/safety/*.cpp
${AIRSIM_ROOT}/AirLib/src/vehicles/car/api/*.cpp
${AIRSIM_ROOT}/AirLib/src/vehicles/multirotor/api/*.cpp
)

# transfer all headers to the include directory
##message("copy the src file ")
##foreach(src ${airsim_source})
##	configure_file(${src} ${PROJECT_SRC_DIR} COPYONLY)
##endforeach()

add_definitions(
  ${PCL_DEFINITIONS}
)

link_directories(
  ${AIRSIM_ROOT}/AirLib/lib
  ${AIRSIM_ROOT}/AirLib/deps/MavLinkCom/lib
  ${AIRSIM_ROOT}/AirLib/deps/rpclib/lib
  ${PCL_LIBRARY_DIRS}
)

add_library( ${PROJECT_NAME} SHARED
    ${airsim_source}
)

target_link_libraries(${PROJECT_NAME}
    AirLib
    MavLinkCom
    rpc
    pthread
)

