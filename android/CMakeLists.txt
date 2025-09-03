cmake_minimum_required(VERSION 3.18)
project(flutter_pdf_render)

# ----------------------------
# bbhelper 库
# ----------------------------
add_library(bbhelper SHARED c++/directBufferAndroid.cpp)
target_compile_options(bbhelper PRIVATE -DBUILD_FOR_ANDROID)
find_library(log-lib log)
target_link_libraries(bbhelper ${log-lib})

# ----------------------------
# flutter_pdf_render 库
# ----------------------------
# 假设插件源码在 src/main/cpp/*.cpp
file(GLOB_RECURSE FLUTTER_PDF_RENDER_SOURCES "c++/directBufferAndroid.cpp")
add_library(flutter_pdf_render SHARED ${FLUTTER_PDF_RENDER_SOURCES})

# 添加链接选项
target_link_options(flutter_pdf_render PRIVATE "-Wl,-z,max-page-size=16384")

# 链接 Android log 库
target_link_libraries(flutter_pdf_render ${log-lib})
