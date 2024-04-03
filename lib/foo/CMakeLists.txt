# 生成库文件
add_library(foo1 foo1.c)
add_library(foo2 foo2.c)

target_link_libraries(foo1 foo_interface)
target_link_libraries(foo2 foo_interface)

if(ECHO_DIR)
    echo_dir()
endif(ECHO_DIR)
