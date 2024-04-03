file(GLOB_RECURSE SRC "*.c" "*.cpp")

add_executable(${PROJECT_NAME} ${SRC})

target_link_libraries(${PROJECT_NAME} ${ALL_LIBS} ${ALL_INCS})

if(ECHO_DIR)
    echo_dir()
endif(ECHO_DIR)
