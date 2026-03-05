cmake_minimum_required(VERSION 3.20)
project(OpenGL_Course LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(glfw3 CONFIG REQUIRED)

# ---- Common GLAD target ----
add_library(glad STATIC glad.c)
target_include_directories(glad PUBLIC
        ${CMAKE_SOURCE_DIR}/include
)

# ---- Common link helper for macOS frameworks ----
set(MAC_GLFW_FRAMEWORKS
        "-framework OpenGL"
        "-framework Cocoa"
        "-framework IOKit"
        "-framework CoreVideo"
)

# Pick the correct GLFW target (Homebrew often provides "glfw")
set(GLFW_TARGET "")
if(TARGET glfw3::glfw)
    set(GLFW_TARGET glfw3::glfw)
elseif(TARGET glfw)
    set(GLFW_TARGET glfw)
else()
    message(FATAL_ERROR "GLFW was found but no usable CMake target (glfw3::glfw or glfw) was exported.")
endif()

# ---- Executable 1: main.cpp ----
add_executable(untitled main.cpp)
target_link_libraries(untitled PRIVATE glad ${GLFW_TARGET} ${MAC_GLFW_FRAMEWORKS})
target_include_directories(untitled PRIVATE ${CMAKE_SOURCE_DIR}/include)

# ---- Executable 2: Lab2.cpp ----
add_executable(Lab2 Lab2.cpp)
target_link_libraries(Lab2 PRIVATE glad ${GLFW_TARGET} ${MAC_GLFW_FRAMEWORKS})
target_include_directories(Lab2 PRIVATE ${CMAKE_SOURCE_DIR}/include)