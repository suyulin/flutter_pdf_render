cmake_minimum_required(VERSION 3.18)
project(flutter_pdf_render)

# ----------------------------
# bbhelper 库
# ----------------------------
add_library(bbhelper SHARED  c++/directBufferAndroid.cpp)
target_compile_options(bbhelper PRIVATE -DBUILD_FOR_ANDROID)
find_library(log-lib log)
target_link_libraries(bbhelper ${log-lib})
target_link_options(bbhelper PRIVATE "-Wl,-z,max-page-size=16384")


