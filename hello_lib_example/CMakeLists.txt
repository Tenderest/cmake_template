get_filename_component(CURRENT_DIR_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)
# message("当前目录名称: ${CURRENT_DIR_NAME}")

# 遍历当前目录下所有的.c和.cpp文件
file(GLOB_RECURSE SRC "*.c" "*.cpp")

# # 跨平台查找当前目录及其子目录下的所有.c和.cpp文件
# file(GLOB_RECURSE SOURCES "*.c;*.cpp")
# # 不论在哪种平台上，以上代码都可以工作
# foreach(SOURCE_FILE ${SOURCES})
#     message("Source file found: ${SOURCE_FILE}")
# endforeach()

# 生成库文件
add_library(${CURRENT_DIR_NAME} SHARED ${SRC})

target_link_libraries(${CURRENT_DIR_NAME} ${CURRENT_DIR_NAME}_proc)
