
SET(CMAKE_BUILD_TYPE "Release")

SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g2 -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")

SET(TARGET_COMPILER "x64")
if(TARGET_COMPILER STREQUAL "x64")
    message(STATUS "TARGET_COMPILE STREQUAL X64")
    SET(NCNN_INSTALL_DIR /opt/external/ncnn/install/x64/)
    SET(ZBAR_INSTALL_DIR /opt/external/zbar-0.10/build/x64/)
    SET(OpenCV_DIR /opt/external/opencv/build/x64)
else()
    message(STATUS "TARGET_COMPILE STREQUAL arm")
    SET(CMAKE_CXX_COMPILER arm-none-linux-gnueabihf-g++)
    SET(CMAKE_C_COMPILER arm-none-linux-gnueabihf-gcc)
    SET(NCNN_INSTALL_DIR /opt/external/ncnn/install/arm/)
    SET(ZBAR_INSTALL_DIR /opt/external/zbar-0.10/build/arm)
    SET(OpenCV_DIR /opt/external/opencv/build/arm)
endif()

PROJECT(ncnnpose)
cmake_minimum_required(VERSION 3.5)

if(OpenCV_FOUND)
 message(OPENCV_VERSION)
endif(OpenCV_FOUND)

find_package(OpenCV REQUIRED)

link_directories(${OpenCV_LIBRARY_DIRS})

include_directories(${OpenCV_INCLUDE_DIRS} )
include_directories(${PROJECT_SOURCE_DIR}/include)
include_directories(${NCNN_INSTALL_DIR}/include/ncnn)

add_executable(ncnnpose ncnnpose.cpp)
target_link_libraries(ncnnpose ${OpenCV_LIBRARIES})
target_link_libraries(ncnnpose ${NCNN_INSTALL_DIR}/lib/libncnn.a -fopenmp)






