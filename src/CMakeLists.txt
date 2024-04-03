# add_executable(ttt test.c)
# add_executable(main main.c)
file(GLOB_RECURSE SRC "*.c" "*.cpp")
add_executable(${PROJECT_NAME} ${SRC})
#                     target lib1 lib2 interface
# target_link_libraries(main   foo1 foo2 foo_interface)

target_link_libraries(${PROJECT_NAME} ${ALL_LIBS} ${ALL_INCS})

if(ECHO_DIR)
    echo_dir()
endif(ECHO_DIR)
