include(CTest)

add_executable(myTest test.cpp)

add_test(NAME myTest COMMAND ${CMAKE_PROJECT_NAME})