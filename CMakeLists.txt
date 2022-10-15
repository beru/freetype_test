cmake_minimum_required(VERSION 3.20)

project(freetype_test)

find_package(freetype REQUIRED)

include_directories(./)

add_executable(freetype_test
	main.cpp
	)

set_target_properties(freetype_test PROPERTIES
	CXX_STANDARD 17
)

target_link_libraries(freetype_test ${FREETYPE_LIBRARIES})
target_include_directories(freetype_test PRIVATE ${FREETYPE_INCLUDE_DIRS})

if(MSVC)
	add_definitions(-D_CRT_SECURE_NO_WARNINGS)
	
	set(bin_path "${FREETYPE_INCLUDE_DIRS}/../../bin/")
	cmake_path(SET bin_path NORMALIZE "${bin_path}")
	set(MY_PATH "PATH=%PATH%" "${bin_path}")
	set_target_properties(freetype_test PROPERTIES
	  VS_STARTUP_PROJECT freetype_test
	  VS_DEBUGGER_ENVIRONMENT "${MY_PATH}"
	  VS_DEBUGGER_COMMAND_ARGUMENTS "msgothic.ttc aiueo"
	  )
	
endif()

