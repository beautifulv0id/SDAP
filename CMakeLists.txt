cmake_minimum_required(VERSION 3.10)
project(EX1)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

find_package(SDPA REQUIRED)

include_directories(${SDPA_INCLUDE_DIRS})

add_executable(${PROJECT_NAME} example.cpp)
target_link_libraries(${PROJECT_NAME} ${SDPA_LIBRARIES})
