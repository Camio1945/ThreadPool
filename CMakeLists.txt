cmake_minimum_required(VERSION 3.26)
project(ThreadPool)

set(CMAKE_CXX_STANDARD 14)

include_directories(.)

add_executable(ThreadPool
        example.cpp
        ThreadPool.h)
