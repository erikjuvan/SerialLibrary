cmake_minimum_required(VERSION 3.11)

project(SerialLibrary)

set(CMAKE_CONFIGURATION_TYPES "Debug;Release") 

set(CMAKE_DEBUG_POSTFIX "-d")

add_library(${PROJECT_NAME} STATIC)

target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_17)

target_include_directories(${PROJECT_NAME} PRIVATE include)

target_link_libraries(${PROJECT_NAME} setupapi)
target_sources(${PROJECT_NAME} PRIVATE
	src/serial.cpp
)

target_sources(${PROJECT_NAME} PRIVATE
	include/serial/serial.h
	include/serial/v8stdint.h
)

if (WIN32)
target_sources(${PROJECT_NAME} PRIVATE
	src/impl/win.cpp
	src/impl/list_ports/list_ports_win.cpp
)

target_sources(${PROJECT_NAME} PRIVATE
	include/serial/impl/win.h
)
endif (WIN32)

if (UNIX)
target_sources(${PROJECT_NAME} PRIVATE
	src/impl/unix.cpp
	src/impl/list_ports/list_ports_linux.cpp
)

target_sources(${PROJECT_NAME} PRIVATE
	include/serial/impl/unix.h
)
endif (UNIX)
