# === version 1.0
# # 做一个可传递的接口
# add_library(hello_interface INTERFACE)
# # message("inc dir: ${CMAKE_CURRENT_SOURCE_DIR}")
# # message("使用了一个可传递的接口作为导入头文件")
# # message("示例 #include \"xxx/xxx.h\"")
# target_include_directories(hello_interface INTERFACE 
#     ${CMAKE_CURRENT_SOURCE_DIR}
# )

# === version 2.0
# 调用函数并将结果存储到变量中
set(SUBDIRECTORIES_LISTS "")
file(GLOB_RECURSE entries LIST_DIRECTORIES true RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *)
foreach(entry ${entries})
    if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/${entry}")
        if(IS_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/${entry}")
            list(APPEND SUBDIRECTORIES_LISTS ${entry})
        endif()
    endif()
endforeach()
# set(${SUBDIRECTORIES_LISTS} ${dirs} PARENT_SCOPE)

# 输出子目录列表
# message("Subdirectories: ${SUBDIRECTORIES_LISTS}")
# message("List of header files: ${SUBDIRECTORIES_LISTS}")
# message("所有头文件目录：${SUBDIRECTORIES_LISTS}")
foreach(SUB_DIR IN LISTS SUBDIRECTORIES_LISTS)
    # message("Found subdirectory: ${SUB_DIR}")
    # message("头文件目录：${SUB_DIR}")
    # message("Found subdirectory name: ${SUB_DIR}")
    message("头文件名称：${SUB_DIR}")
    # 对头文件目录做成 Interface 接口传递出去
    # 做一个可传递的接口
    add_library(${SUB_DIR}_interface INTERFACE)
    target_include_directories(${SUB_DIR}_interface INTERFACE 
        ${CMAKE_CURRENT_SOURCE_DIR}
    )
    message("目标对应的接口名称：${SUB_DIR}_interface")
    list(APPEND ALL_INCS_NAME ${SUB_DIR}_interface)
endforeach()

set(ALL_INCS ${ALL_INCS_NAME} PARENT_SCOPE)

# 计算子目录数量
# list(LENGTH SUBDIRECTORIES_LISTS subdir_count)
# message("Number of subdirectories: ${subdir_count}")

if(ECHO_DIR)
    echo_dir()
endif(ECHO_DIR)
