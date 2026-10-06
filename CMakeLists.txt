cmake_minimum_required(VERSION 3.24)

# Turing (RTX 2070 Super) and Blackwell (RTX 5070). Override with -DCMAKE_CUDA_ARCHITECTURES=...
if(NOT DEFINED CMAKE_CUDA_ARCHITECTURES)
    set(CMAKE_CUDA_ARCHITECTURES 75 120)
endif()

project(pathtracer LANGUAGES CXX CUDA)

# Benchmark numbers only mean something in Release.
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
endif()

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_CUDA_STANDARD_REQUIRED ON)

add_executable(pathtracer
    src/main.cu
)

target_include_directories(pathtracer PRIVATE src)

# -lineinfo maps SASS back to source lines in Nsight Compute without disabling optimizations.
target_compile_options(pathtracer PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:-lineinfo>)
