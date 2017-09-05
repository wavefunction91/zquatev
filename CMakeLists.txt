cmake_minimum_required(VERSION 3.0)
project(ZQUATEV CXX)
set(ZQUATEV_VERSION_MAJOR 0)
set(ZQUATEV_VERSION_MINOR 1)
set(ZQUATEV_VERSION_PATCH 0)

# C++11
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 11)

# Define include directories
include_directories("${PROJECT_SOURCE_DIR}/include")

# Handle MKL for ZGEMM3M + C++11
if(${CMAKE_CXX_COMPILER} MATCHES "icpc.*$")
  message(STATUS "INTEL COMPILER")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -mkl=parallel -std=c++11")
  set(_HAS_MKL 1)
else()
  set(LA_LINK lapack blas)
endif()

add_subdirectory(src)
add_subdirectory(tests)



install(FILES ${PROJECT_SOURCE_DIR}/include/f77.h DESTINATION include)
install(FILES ${PROJECT_SOURCE_DIR}/include/supermat.h DESTINATION include)
install(FILES ${PROJECT_SOURCE_DIR}/include/zquatev.h DESTINATION include)
