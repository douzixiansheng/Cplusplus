# 指定生成目标
add_executable(plus "src/main.cpp")
# 生成链接库
add_library(libplus SHARED "src/a.cpp")

# 对目标库进行链接操作,如果有需要链接的库文件的时候才进行操作,如果该文件没有库文件,则不需要该命令.
# 该命令一般在 add_executable后面
target_link_libraries(libplus ${CONAN_LIBS_LUA} ${CONAN_LIBS_OPENSSL})
#target_link_libraries(plus libplus)

REDIRECT_OUTPUT(plus ${MY_BIN_PATH})
REDIRECT_OUTPUT(libplus ${MY_BIN_PATH})

if(UNIX)
    target_link_libraries(libplus pthread -static-libgcc -static-libstdc++)
else()
    set_target_properties(libplus PROPERTIES LINK_FLAGS /ignore:4099)
endif()