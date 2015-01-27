# This is to see wether the library compiles correctly:
#try_compile(COMPILE_SUCCEEDED ${CMAKE_BINARY_DIR}/compile_tests my_test_src.cpp)

#if(COMPILE_SUCCEEDED)
#  message("Success!")
#endif()

cmake_minimum_required (VERSION 2.6)

enable_testing()

file(GLOB _test_files ${CMAKE_SOURCE_DIR}/test/*cc)

foreach(_test ${_test_files})
GET_FILENAME_COMPONENT(_test_name ${_test} NAME_WE)
# test:
MESSAGE("Testing ${_test_name}, with file ${_test}")
add_executable(${_test_name}.exe ${_test})
add_test (${_test_name} ${_test_name}.exe)
add_test (${_test_name} ${CMAKE_COMMAND} -E compare_files 
	  ${_test_name}.output temp.output)
endforeach()
