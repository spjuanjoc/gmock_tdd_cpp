cmake_minimum_required(VERSION 3.15)
project(gmock_demo3)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread ")

# for googletest
add_definitions(-DGTEST_LANGUAGE_CXX11)
enable_testing()

set(SOURCES
        main.cpp
        Module/Module.cpp
        Module/Logic.cpp
        test/Module/TestLogic.cpp
        )

# To get the headers
include_directories(Module)
include_directories(test/Module)

#To compile with coverage
if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    message("System name: ${CMAKE_SYSTEM_NAME}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --coverage ")#-fprofile-arcs -ftest-coverage")
endif()

add_executable(${PROJECT_NAME} ${SOURCES})

# Link googletest with the current project
target_link_libraries(${PROJECT_NAME} gtest gmock)
