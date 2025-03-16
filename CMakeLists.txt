cmake_minimum_required(VERSION 3.10)
project(GameEngine)

set(CMAKE_CXX_STANDARD 17)

# Enable FetchContent if you want an alternative to submodules
include(FetchContent)

# Add subdirectories for each of the libraries
add_subdirectory(third_party_libs/openal-soft)
add_subdirectory(third_party_libs/bgfx)
add_subdirectory(third_party_libs/imgui)
add_subdirectory(third_party_libs/box2d)
add_subdirectory(third_party_libs/sdl)

# Create the main game engine executable
add_executable(GameEngine src/main.cpp)

# Include directories for each library
target_include_directories(GameEngine PRIVATE
    third_party_libs/openal-soft/include
    third_party_libs/bgfx/include
    third_party_libs/imgui
    third_party_libs/box2d
    third_party_libs/sdl/include
)

# Link libraries to your game engine executable
target_link_libraries(GameEngine PRIVATE 
    OpenAL
    bgfx
    imgui
    box2d
    SDL2
)

# If you need to link OpenGL (for bgfx)
find_package(OpenGL REQUIRED)
target_link_libraries(GameEngine PRIVATE OpenGL::GL)
