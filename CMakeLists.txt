cmake_minimum_required(VERSION 3.17)
project(App)

set(CMAKE_CXX_STANDARD 14)
set(APP_TARGET App) # Target Name

## SDL2
set(sdl2_Includes "${PROJECT_SOURCE_DIR}/sdl2/include")
set(SDL2_LibDir "${PROJECT_SOURCE_DIR}/sdl2/lib")
set(SDL2_Libs mingw32 SDL2main SDL2 winmm imm32 version setupapi)
add_library(SDL2 STATIC IMPORTED)
add_library(SDL2main STATIC IMPORTED)
set_property(TARGET SDL2 PROPERTY IMPORTED_LOCATION "${SDL2_LibDir}/libSDL2.a")
set_property(TARGET SDL2main PROPERTY IMPORTED_LOCATION "${SDL2_LibDir}/libSDL2main.a")


## Gl3W
set(gl3w_Includes "gl3w/include")
add_library(gl3w STATIC gl3w/gl3w.c)

## Imgui lib
set(imgui_Includes "imgui/include")
add_library(imgui STATIC
        imgui/imgui.cpp
        imgui/imgui_widgets.cpp
        imgui/imgui_draw.cpp
        imgui/imgui_demo.cpp
        imgui/imgui_impl_sdl.cpp
        imgui/imgui_impl_opengl3.cpp)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -lmingw32")
set(CMAKE_EXE_LINKER_FLAGS "-static-libgcc -static-libstdc++")
set(SOURCE_FILES src/main.cpp) # Source files
include_directories(${gl3w_Includes} ${sdl2_Includes} ${imgui_Includes})

add_executable(${APP_TARGET} ${SOURCE_FILES}) # Executable
target_link_libraries(${APP_TARGET} imgui gl3w ${SDL2_Libs} )
