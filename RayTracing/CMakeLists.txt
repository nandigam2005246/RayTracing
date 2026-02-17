cmake_minimum_required(VERSION 3.22)

project(RayTracing)


set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin/$<CONFIG>)

file(GLOB SOURCE_FILES
    "${CMAKE_CURRENT_SOURCE_DIR}/Source/*.cpp"
)

file(GLOB HEADER_FILES
    "${CMAKE_CURRENT_SOURCE_DIR}/Header/*.h"
	"${CMAKE_CURRENT_SOURCE_DIR}/Header/*.hpp"
)

# add source filters
source_group("Source" FILES ${SOURCE_FILES})

# add header filters
source_group("Header" FILES ${HEADER_FILES})

add_executable(RayTracing ${SOURCE_FILES} ${HEADER_FILES})

# collect all include file paths
set(INCLUDE_FILE_PATHS  "${CMAKE_CURRENT_SOURCE_DIR}/Header"
)

# collect all linker file paths
#set(TESTS_LINK_FILE_PATHS
#)

# add include file paths
target_include_directories(RayTracing PRIVATE ${INCLUDE_FILE_PATHS})

# add linker file paths
#target_link_libraries(RayTracing PRIVATE ${TESTS_LINK_FILE_PATHS})

set_target_properties(RayTracing  PROPERTIES
	VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}"
)

set_target_properties(RayTracing  PROPERTIES
	LIBRARY_OUTPUT_DIRECTORY "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}"
)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    PROPERTY VS_STARTUP_PROJECT RayTracing
)
