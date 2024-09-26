cmake_minimum_required(VERSION 3.29)
project(openGLx)

set(CMAKE_CXX_STANDARD 20)

# Include directories for GLFW and ImGui
include_directories(${PROJECT_SOURCE_DIR}/libs/GLFW/include)
include_directories(${PROJECT_SOURCE_DIR}/libs)
include_directories(${PROJECT_SOURCE_DIR}/imguiH)

# Ensure ARM64 architecture on Apple Silicon (M1/M2)
if (APPLE)
    set(CMAKE_OSX_ARCHITECTURES "arm64")
endif()

# Add executable (source files only)
add_executable(openGLx main.cpp
        libs/imgui_impl_opengl3.cpp
        libs/imgui_impl_glfw.cpp
        imguiC/imgui.cpp
        imguiC/imgui_draw.cpp
        imguiC/imgui_demo.cpp
        imguiC/imgui_tables.cpp
        imguiC/imgui_widgets.cpp)

# Find OpenGL package
find_package(OpenGL REQUIRED)

# Link OpenGL, GLFW, and macOS frameworks
target_link_libraries(${PROJECT_NAME}
        ${OPENGL_gl_LIBRARY}
        "${PROJECT_SOURCE_DIR}/libs/libglfw3.a"
        "-framework CoreFoundation"
        "-framework Cocoa"
        "-framework OpenGL"
        "-framework IOKit"
)