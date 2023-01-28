cmake_minimum_required(VERSION 3.24)
project(sdl_demo C)

set(CMAKE_C_STANDARD 17)

# Find SDL2
find_package(SDL2 REQUIRED)

add_executable(sdl_demo src/main.c)
