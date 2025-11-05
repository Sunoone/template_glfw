cmake_minimum_required(VERSION 3.10...4.0)
project(opengl_application)

set(CMAKE_C_STANDARD 90)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE) 
set(EXTERNAL_PATH "${CMAKE_CURRENT_SOURCE_DIR}/external")

# Include directories for Glad and GLFW
include_directories(
    ${EXTERNAL_PATH}/glad/include
    ${EXTERNAL_PATH}/glfw/include
)
add_subdirectory(${EXTERNAL_PATH}/glfw ${CMAKE_BINARY_DIR}/glfw)

add_executable(opengl_application src/main.c ${EXTERNAL_PATH}/glad/src/glad.c)

# Link SDL3 statically
set(GLFW_BUILD_SHARED_LIBS OFF CACHE BOOL "Build GLFW as a static library.")
target_link_libraries(opengl_application glfw)

# if(UNIX)
    find_package(OpenGL REQUIRED)
    target_link_libraries(opengl_application ${OPENGL_LIBRARIES})
# endif()
