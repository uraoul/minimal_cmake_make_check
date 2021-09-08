cmake_minimum_required(VERSION 3.14)

project(cmake_make_check)
add_executable (foo main.cxx)

include(CTest)
enable_testing()
# emulate autotools make check
# see https://gitlab.kitware.com/cmake/community/-/wikis/doc/tutorials/EmulateMakeCheck
set(CMAKE_CTEST_COMMAND ctest -T test)
add_custom_target(check COMMAND ${CMAKE_CTEST_COMMAND})
add_executable(mytest EXCLUDE_FROM_ALL mytest.cxx)
add_test(mytest mytest)
add_dependencies(check mytest)

install(TARGETS foo DESTINATION bin)

