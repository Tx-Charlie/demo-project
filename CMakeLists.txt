cmake_minimum_required(VERSION 3.10)

project(demo)

if(MSVC OR WIN32)
	set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
	set(BUILD_SHARED_LIBS TRUE)
endif()

# lib
set(PROJECT_LIB func)
file(GLOB_RECURSE LIB_SRC lib/*.cpp)
add_library(${PROJECT_LIB} SHARED ${LIB_SRC})
target_include_directories(${PROJECT_LIB} PUBLIC lib)

# demo exec
file(GLOB_RECURSE SRC src/*.cpp)
add_executable(${PROJECT_NAME} ${SRC})
target_include_directories(${PROJECT_NAME} PUBLIC lib src)
target_link_libraries(${PROJECT_NAME} PUBLIC ${PROJECT_LIB})
