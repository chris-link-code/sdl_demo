cmake_minimum_required(VERSION 3.24)
project(sdl_demo C)

message("")
message(STATUS "CMAKE_BINARY_DIR: " ${CMAKE_BINARY_DIR})
message(STATUS "CMAKE_SOURCE_DIR: " ${CMAKE_SOURCE_DIR})
message(STATUS "CMAKE_COMMAND: " ${CMAKE_COMMAND})
message(STATUS "CMAKE_VERSION: " ${CMAKE_VERSION})
message(STATUS "CMAKE_C_COMPILER: " ${CMAKE_C_COMPILER})
message(STATUS "CMAKE_PROJECT_NAME: " ${CMAKE_PROJECT_NAME})
message(STATUS "CMAKE_FINDCMAKE: " ${CMAKE_SOURCE_DIR}/CMAKE)

set(CMAKE_C_STANDARD 17)


# ------- Set Vars ------- #

#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/CMAKE")
set(SOURCE_FILES src/main.c)

message("")
message(STATUS "SOURCE entry point : " ${SOURCE_FILES})
message("")

# ------- End Set Vars --- #


# ------- Executable ----- #

add_executable(sdl_demo src/main.c)
#ADD_EXECUTABLE(SDL2_Basic_Setup ${SOURCE_FILES})

# ------- End Executable - #


# ------- Finds ---------- #

# Find SDL2
find_package(SDL2 REQUIRED)

message("")
message(STATUS "FINDING SDL2")
IF (${SDL2_FOUND})
    message(STATUS "SDL2_FOUND: " ${SDL2_FOUND})
    message(STATUS "SDL2_INCLUDE_DIR:" ${SDL2_INCLUDE_DIR})
    message(STATUS "SDL2_LIBRARY: " ${SDL2_LIBRARY})
ELSE ()
    message(STATUS "SDL2_FOUND: " ${SDL2_FOUND})
    message(FATAL_ERROR "SDL2 NOT FOUND")
ENDIF ()

find_package(SDL2_IMAGE)
message("")
message(STATUS "FINDING SDL2_IMAGE")
message(STATUS "SDL2_IMAGE_FOUND: " ${SDL2_IMAGE_FOUND})

IF (${SDL2_IMAGE_FOUND})
    message(STATUS "SDL2_IMAGE_INCLUDE_DIR: " ${SDL2_IMAGE_INCLUDE_DIR})
    message(STATUS "SDL2_IMAGE_LIBRARY: " ${SDL2_IMAGE_LIBRARY})
ELSE ()
    message(FATAL_ERROR "SDL2_IMAGE NOT FOUND")
ENDIF ()

find_package(SDL2_TTF)
message("")
message(STATUS "FINDING SDL2TTF")
message(STATUS "SDL2TTF_FOUND: " ${SDL2TTF_FOUND})

IF (${SDL2_TTF_FOUND})
    message(STATUS "SDL2TTF_INCLUDE_DIR: " ${SDL2TTF_INCLUDE_DIR})
    message(STATUS "SDL2TTF_LIBRARY: " ${SDL2TTF_LIBRARY})
ELSE ()
    message(FATAL_ERROR "SDL2TTF NOT FOUND")
ENDIF ()
message("")

find_package(SDL2_Mixer)

message(STATUS "FINDING SDL2Mixer")
message(STATUS "SDL2Mixer_FOUND: " ${SDL2_Mixer_FOUND})

message("")

#file(COPY resources DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})

# ------- End Finds ------ #

# ------- Inc & Link ---- #

include_directories(${SDL2_INCLUDE_DIR} ${SDL2TTF_INCLUDE_DIR} ${SDL2_IMAGE_INCLUDE_DIR} ${SDL2Mixer_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARY} ${SDL2TTF_LIBRARY} ${SDL2_IMAGE_LIBRARY} ${SDL2Mixer_LIBRARY})

# ------- End ----------- #
