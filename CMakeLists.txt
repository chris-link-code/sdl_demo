cmake_minimum_required(VERSION 3.24)
project(sdl_demo C)

message("")
message(STATUS "cmake_binary_dir: " ${CMAKE_BINARY_DIR})
message(STATUS "cmake_source_dir: " ${CMAKE_SOURCE_DIR})
message(STATUS "cmake_command: " ${CMAKE_COMMAND})
message(STATUS "cmake_version: " ${CMAKE_VERSION})
message(STATUS "cmake_c_compiler: " ${CMAKE_C_COMPILER})
message(STATUS "cmake_project_name: " ${CMAKE_PROJECT_NAME})
#message(STATUS "cmake_find_cmake: " ${CMAKE_SOURCE_DIR}/CMAKE)

set(CMAKE_C_STANDARD 17)


# ------- Set Vars ------- #

#set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/CMAKE")

#set(SOURCE_FILE src/main.c)
set(SOURCE_FILE src/basic_setup.c)

message("")
message(STATUS "start source file: " ${SOURCE_FILE})

# ------- End Set Vars --- #


# ------- Executable ----- #

add_executable(sdl_demo ${SOURCE_FILE})
#ADD_EXECUTABLE(SDL2_Basic_Setup ${SOURCE_FILE})

# ------- End Executable - #


# ------- Finds ---------- #
# finding SDL2
find_package(SDL2 REQUIRED)
message("")
message(STATUS "finding SDL2")
IF (${SDL2_FOUND})
    message(STATUS "SDL2_found: " ${SDL2_FOUND})
    message(STATUS "SDL2_include_dirs: " ${SDL2_INCLUDE_DIRS})
    message(STATUS "SDL2_libraries: " ${SDL2_LIBRARIES})
    message(STATUS "SDL2_version: " ${SDL2_VERSION})
ELSE ()
    message(FATAL_ERROR "SDL2 NOT FOUND")
ENDIF ()

# finding SDL2_IMAGE
find_package(SDL2_IMAGE REQUIRED)
message("")
message(STATUS "finding SDL2_IMAGE")
IF (${SDL2_IMAGE_FOUND})
    message(STATUS "SDL2_image_found: " ${SDL2_IMAGE_FOUND})
    #    message(STATUS "SDL2_IMAGE_include_dirs: " ${SDL2_IMAGE_INCLUDE_DIRS})
    #    message(STATUS "SDL2_IMAGE_libraries: " ${SDL2_IMAGE_LIBRARIES})
    message(STATUS "SDL2_image_version: " ${SDL2_IMAGE_VERSION})
ELSE ()
    message(FATAL_ERROR "SDL2_IMAGE NOT FOUND")
ENDIF ()

# finding SDL2_TTF
find_package(SDL2_TTF REQUIRED)
message("")
message(STATUS "finding SDL2_TTF")
IF (${SDL2_TTF_FOUND})
    message(STATUS "SDL2_TTF_found: " ${SDL2_TTF_FOUND})
    #    message(STATUS "SDL2_TTF_include_dirs: " ${SDL2_TTF_INCLUDE_DIRS})
    #    message(STATUS "SDL2_TTF_libraries: " ${SDL2_TTF_LIBRARIES})
    message(STATUS "SDL2_TTF_version: " ${SDL2_TTF_VERSION})
ELSE ()
    message(FATAL_ERROR "SDL2_TTF NOT FOUND")
ENDIF ()

# finding SDL2_Mixer
find_package(SDL2_Mixer REQUIRED)
message("")
message(STATUS "finding SDL2_Mixer")
IF (${SDL2_Mixer_FOUND})
    message(STATUS "SDL2_Mixer_found: " ${SDL2_TTF_FOUND})
    #        message(STATUS "SDL2_Mixer_include_dirs: " ${SDL2_Mixer_INCLUDE_DIRS})
    #        message(STATUS "SDL2_Mixer_libraries: " ${SDL2_Mixer_LIBRARIES})
    message(STATUS "SDL2_Mixer_version: " ${SDL2_Mixer_VERSION})
ELSE ()
    message(FATAL_ERROR "SDL2_Mixer NOT FOUND")
ENDIF ()

message("")

#file(COPY resources DESTINATION ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})

# ------- End Finds ------ #

# ------- Inc & Link ---- #

include_directories(
        ${SDL2_INCLUDE_DIRS}
        ${SDL2TTF_INCLUDE_DIR}
        ${SDL2_IMAGE_INCLUDE_DIR}
        ${SDL2Mixer_INCLUDE_DIR}
)
target_link_libraries(
        ${PROJECT_NAME}
        ${SDL2_LIBRARIES}
        ${SDL2TTF_LIBRARY}
        ${SDL2_IMAGE_LIBRARY}
        ${SDL2Mixer_LIBRARY}
)

# 隐藏控制台
set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} -mwindows)

# ------- End ----------- #
