cmake_minimum_required(VERSION 2.8.11)
project(ThreedBeamFEA)

if (NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, default to Release")
    set(CMAKE_BUILD_TYPE "Release")
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")

#include(FindOpenMP)
#if(OPENMP_FOUND)
#  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS} -O3 -fopenmp")
#endif(OPENMP_FOUND)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/bin)

set(EXT_BOOST_ROOT ${CMAKE_CURRENT_LIST_DIR}/ext/boost-1.65.1)
set(EXT_EIGEN_ROOT ${CMAKE_CURRENT_LIST_DIR}/ext/eigen-3.3.4)
set(EXT_RAPIDJSON_ROOT ${CMAKE_CURRENT_LIST_DIR}/ext/rapidjson-1.1.0/include)
set(EXT_TCLAP_ROOT ${CMAKE_CURRENT_LIST_DIR}/ext/tclap-1.2.1/include)

#include_directories(${EXT_BOOST_ROOT})
add_library(${PROJECT_NAME} src/cmd.cpp src/setup.cpp src/summary.cpp src/threed_beam_fea.cpp)

target_include_directories(${PROJECT_NAME}
    PRIVATE ${CMAKE_CURRENT_LIST_DIR}/include/
    PUBLIC ${EXT_BOOST_ROOT}
    PRIVATE ${EXT_EIGEN_ROOT}
    PRIVATE ${EXT_RAPIDJSON_ROOT}
    PRIVATE ${EXT_TCLAP_ROOT}
                    )
