cmake_minimum_required(VERSION 3.10)
project(EX1)

set(SDPA_DIR ${CMAKE_CURRENT_SOURCE_DIR}/..)

set(LAPACK_DIR ${SDPA_DIR}/external_libs/lapack-3.9.0/)
set(LAPACK_INCLUDE_DIR ${LAPACK_DIR}/LAPACKE/include)
set(CBLAS_DIR ${SDPA_DIR}/external_libs/lapack-3.9.0/CBLAS)
set(CBLAS_INCLUDE_DIR ${CBLAS_DIR}/include)

include_directories(${LAPACK_INCLUDE_DIR} ${CBLAS_INCLUDE_DIR})

add_executable(${PROJECT_NAME} example1.cpp)
target_link_libraries(${PROJECT_NAME} ${LAPACK_DIR}/liblapack.a ${SDPA_DIR}/libsdpa.a)
