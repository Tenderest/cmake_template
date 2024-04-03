# add_executable(ttt test.c)
# add_executable(main main.c)
add_executable(${PROJECT_NAME} main.c)
#                     target lib1 lib2 interface
# target_link_libraries(main   foo1 foo2 foo_interface)
target_link_libraries(${PROJECT_NAME} foo1 foo2 foo_interface)

if(ECHO_DIR)
    echo_dir()
endif(ECHO_DIR)
