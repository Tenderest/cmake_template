set(SUB_ALL_LIBS "")
# Linux 版本获取当前目录的所有子目录
function(get_current_directories_linux)
    execute_process(
        COMMAND find ${CMAKE_CURRENT_SOURCE_DIR} -maxdepth 1 -type d ! -name . -not -path "./.*" ! -wholename ${CMAKE_CURRENT_SOURCE_DIR}
        OUTPUT_VARIABLE SUBDIRECTORIES
        OUTPUT_STRIP_TRAILING_WHITESPACE
        ERROR_VARIABLE ERRORS
    )

    if(ERRORS)
        message("Error occurred while finding subdirectories: ${ERRORS}")
    else()
        if (SUBDIRECTORIES)
            string(REPLACE "\n" ";" SUBDIRECTORIES_LIST ${SUBDIRECTORIES})

            foreach(DIR IN LISTS SUBDIRECTORIES_LIST)
                message("库文件路径：${DIR}")
                # 对目录名称做截取，去掉前面的路径
                get_filename_component(DIR_NAME ${DIR} NAME)
                message("库文件名称：${DIR_NAME}")
                add_subdirectory(${DIR_NAME})
                # 追加名称到一个函数中的缓存列表
                list(APPEND ALL_LIBS_NAME ${DIR_NAME})
            endforeach()

            # 将更新后的列表赋值回父作用域，函数外
            set(SUB_ALL_LIBS ${ALL_LIBS_NAME} PARENT_SCOPE)
        else()
            message("No subdirectories found in 'lib' directory.")
        endif()
    endif()
endfunction(get_current_directories_linux)

# Windows 版本获取当前目录的所有子目录
function(get_current_directories_windows)
    execute_process(
        COMMAND cmd /c dir /ad /b
        WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
        OUTPUT_VARIABLE SUBDIRECTORIES
        OUTPUT_STRIP_TRAILING_WHITESPACE
        ERROR_VARIABLE ERRORS
    )

    if(ERRORS)
        message("Error occurred while finding subdirectories: ${ERRORS}")
    else()
        string(REPLACE "\r\n" ";" SUBDIRECTORIES_LIST ${SUBDIRECTORIES})
        list(REMOVE_ITEM SUBDIRECTORIES_LIST .)
        foreach(DIR IN LISTS SUBDIRECTORIES_LIST)
            message("库文件路径：${DIR}")
            # 对目录名称做截取，去掉前面的路径
            get_filename_component(DIR_NAME ${DIR} NAME)
            message("库文件名称：${DIR_NAME}")
            add_subdirectory(${DIR_NAME})
            # 追加名称到一个函数中的缓存列表
            list(APPEND ALL_LIBS_NAME ${DIR_NAME})
        endforeach()
        # 将更新后的列表赋值回父作用域，函数外
        set(SUB_ALL_LIBS ${ALL_LIBS_NAME} PARENT_SCOPE)
    endif()   
endfunction(get_current_directories_windows)

# 遍历当前目录的所有子目录，并 add_subdirecotry()
if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    # 在Linux环境下执行的操作
    get_current_directories_linux()
    # 更新父作用域变量的值，文件外
    set(ALL_LIBS ${SUB_ALL_LIBS} PARENT_SCOPE)
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    # 在Windows环境下执行的操作
    get_current_directories_windows()
    set(ALL_LIBS ${SUB_ALL_LIBS} PARENT_SCOPE)
else()
    message(WARNING "Unsupported operating system.")
endif()

if(ECHO_DIR)
    echo_dir()
endif(ECHO_DIR)
