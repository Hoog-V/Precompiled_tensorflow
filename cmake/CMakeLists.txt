cmake_minimum_required(VERSION 3.16)
# Double colon in target name means ALIAS or IMPORTED target.
cmake_policy(SET CMP0028 NEW)
# Enable MACOSX_RPATH (@rpath) for built dynamic libraries.
cmake_policy(SET CMP0042 NEW)
project(tensorflow-lite C CXX)

add_library(tensorflow-lite INTERFACE)

target_include_directories(tensorflow-lite INTERFACE ${CMAKE_CURRENT_LIST_DIR}/inc)

if(${CMAKE_SYSTEM_NAME} STREQUAL "Windows")
    target_link_libraries(tensorflow-lite INTERFACE ${CMAKE_CURRENT_LIST_DIR}/lib/tensorflowlite.dll.if.lib)
    file(COPY ${CMAKE_CURRENT_LIST_DIR}/lib/tensorflowlite.dll DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
else()
    target_link_libraries(tensorflow-lite INTERFACE ${CMAKE_CURRENT_LIST_DIR}/lib/libtensorflowlite.so)
endif()

