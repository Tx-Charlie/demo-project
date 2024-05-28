cmake_minimum_required(VERSION 3.10)

project(demo)

# project setup
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_COMPILER_LAUNCHER ccache)

# clang-tidy during build
# set(CMAKE_CXX_CLANG_TIDY 
#   clang-tidy;
#   -header-filter=.;
#   -checks=*;
#   -warnings-as-errors=*;)

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

# install
# headers 
# install(FILES ${CMAKE_BINARY_DIR}/include/xxx DESTINATION include)
install(TARGETS 
  ${PROJECT_NAME}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin)

# uninstall
if (NOT TARGET uninstall)
  configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
    IMMEDIATE @ONLY)
  add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake)
endif()
