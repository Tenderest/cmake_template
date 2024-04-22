file(GLOB_RECURSE SRC "*.c" "*.cpp")

# add_executable(${PROJECT_NAME} ${SRC})

# target_link_libraries(${PROJECT_NAME} ${ALL_LIBS} ${ALL_INCS})

foreach(FILE ${SRC})
    get_filename_component(BASE_NAME ${FILE} NAME)
    # string(SUBSTRING ${BASE_NAME} 0 4 BASE_NAME)
    string(FIND ${BASE_NAME} "." comma_pos) # 找到逗号的位置
    if(NOT ${comma_pos} EQUAL -1) # 如果找到了逗号
    string(SUBSTRING ${BASE_NAME} 0 ${comma_pos} BASE_NAME)
    else()
    # 如果没有找到逗号，保持原样
    endif()
    # message("Source files: ${BASE_NAME}")
    add_executable(${BASE_NAME} ${FILE})
    target_link_libraries(${BASE_NAME} ${ALL_LIBS} ${ALL_INCS})
endforeach(FILE ${SRC})

