cmake_minimum_required(VERSION 3.5)

if(BUILD_WINDOWS)
	set(CMAKE_TOOLCHAIN_FILE "${CMAKE_SOURCE_DIR}/windows_toolchain.cmake")
	set(VIDEO_OPENGLES OFF CACHE BOOL "whatever")
	add_definitions(-DBUILD_WINDOWS)
endif(BUILD_WINDOWS)

project(SDL_test)

option(BUILD_WINDOWS "Build Windows" OFF)

set(CMAKE_CXX_STANDARD 14)

add_subdirectory(SDL2)

file(GLOB source "main.cpp")

set(CMAKE CXX_FLAGS "${CMAKE_CXX_FLAGS} ${SDL2_CFLAGS_LIBS}")

add_executable(ufo WIN32 ${source})
target_include_directories(ufo PUBLIC SDL2/include)
target_link_libraries(ufo SDL2-static)

set(CMAKE_EXE_LINKER_FLAGS "-static-libgcc -static-libstdc++")

