# 搜索当前目录的所有子目录
set(SUBDIRECTORIES_LISTS "")
file(GLOB_RECURSE entries LIST_DIRECTORIES true RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *)
foreach(entry ${entries})
    if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/${entry}")
        if(IS_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/${entry}")
            list(APPEND SUBDIRECTORIES_LISTS ${entry})
        endif()
    endif()
endforeach()

# 处理子目录列表
foreach(SUB_DIR IN LISTS SUBDIRECTORIES_LISTS)
    message("头文件名称：${SUB_DIR}")
    add_library(${SUB_DIR}_proc INTERFACE)
    target_include_directories(${SUB_DIR}_proc INTERFACE 
        ${CMAKE_CURRENT_SOURCE_DIR}
    )
    message("目标对应的接口名称：${SUB_DIR}_proc")
    list(APPEND ALL_INCS_NAME ${SUB_DIR}_proc)
endforeach()

# 更新父作用域变量的值，文件外
set(ALL_INCS ${ALL_INCS_NAME} PARENT_SCOPE)

# 计算子目录数量
# list(LENGTH SUBDIRECTORIES_LISTS subdir_count)
# message("Number of subdirectories: ${subdir_count}")
