cmake_minimum_required(VERSION 3.20)
project(OpenGL_Course LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(glfw3 CONFIG REQUIRED)

add_executable(untitled
        main.cpp
        glad.c
)

target_include_directories(untitled PRIVATE
        ${CMAKE_SOURCE_DIR}/include
)

# Pick the correct GLFW target (Homebrew often provides "glfw")
if(TARGET glfw3::glfw)
    target_link_libraries(untitled PRIVATE glfw3::glfw)
elseif(TARGET glfw)
    target_link_libraries(untitled PRIVATE glfw)
else()
    message(FATAL_ERROR "GLFW was found but no usable CMake target (glfw3::glfw or glfw) was exported.")
endif()

# macOS: you usually also need these frameworks for OpenGL + windowing
target_link_libraries(untitled PRIVATE
        "-framework OpenGL"
        "-framework Cocoa"
        "-framework IOKit"
        "-framework CoreVideo"
)