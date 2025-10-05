cmake_minimum_required(VERSION 3.16)
project(shelly_proto LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(SDL_VIDEO_DRIVER_KMSDRM 1)
set(SDL_VIDEO_DRIVER_WAYLAND 0)
set(SDL_VIDEO_DRIVER_X11 0)

# Build options
option(CHERRY_STATIC "Link Cherry statically" OFF)
option(CHERRY_DEBUG "Enable Cherry debug tools" OFF)
option(CHERRY_PACKAGE "Enable packaging features with pyinstaller" OFF)

# Cherry Options & Addons
option(CHERRY_ENABLE_NET "Enable net features" OFF)
option(CHERRY_ENABLE_CEF "Enable chrome embedded framwork (CEF)" OFF)
option(CHERRY_ENABLE_AUDIO "Enable audio features" OFF)
option(CHERRY_ENABLE_LINUXDRM "Enable Linux Direct Rendering Manager" ON)

# Cherry Optimizations
option(CHERRY_DISABLE_NODES "Disable nodal systems" OFF)
option(CHERRY_DISABLE_WORKSPACESAVES "Disable workspace saves" OFF)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib/cherry)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/lib/cherry cherry_build)
add_executable(shelly_proto src/main.cpp)
target_link_libraries(shelly_proto PRIVATE cherry)