# CMake 最低版本号要求
cmake_minimum_required (VERSION 3.0.0)

# 项目信息
project (Plus LANGUAGES C CXX)

# c++ 17
set(CMAKE_CXX_STANDARD 17)
# 设置指定的C++编译版本是必须的 如果不设置或者为off，则指定版本不可用时，会使用上一个版本
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# windows options
if (WIN32)
    # 设置编译器选项
    add_compile_options(-D_WIN32_WINNT=0x0601)
    # add_definitions 用于添加编译参数
    add_definitions(/wd4819 /wd4244 /wd4200 /wd4996 /bigobj)
# linux options
else()
    add_compile_options(-fPIC)

    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -O0 -ggdb")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -g")
endif()

# 添加 src 子目录
add_subdirectory(src)