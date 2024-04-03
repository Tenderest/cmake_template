# 做一个可传递的接口
add_library(foo_interface INTERFACE)
# message("inc dir: ${CMAKE_CURRENT_SOURCE_DIR}")
# message("使用了一个可传递的接口作为导入头文件")
# message("示例 #include \"xxx/xxx.h\"")
target_include_directories(foo_interface INTERFACE 
    ${CMAKE_CURRENT_SOURCE_DIR}
)

if(ECHO_DIR)
    echo_dir()
endif(ECHO_DIR)
