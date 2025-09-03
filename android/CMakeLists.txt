cmake_minimum_required(VERSION 3.4.1)

add_library(bbhelper SHARED c++/directBufferAndroid.cpp)
target_link_options(${CMAKE_PROJECT_NAME} PRIVATE "-Wl,-z,max-page-size=16384")

target_compile_options(bbhelper PRIVATE -DBUILD_FOR_ANDROID)
