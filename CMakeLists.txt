cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

# project name
project(tinycbor)

# library name
add_library(tinycbor)
add_library(intel::tinycbor ALIAS tinycbor)

target_sources(tinycbor PRIVATE
    src/cborerrorstrings.c
	src/cborencoder.c
	src/cborencoder_close_container_checked.c
	src/cborencoder_float.c
	src/cborparser.c
	src/cborparser_float.c
	src/cborpretty.c
	src/cborparser_dup_string.c
	src/cborpretty_stdio.c
	src/cbortojson.c
	src/cborvalidation.c)
target_include_directories(tinycbor PUBLIC src)

if(WIN32)
    add_definitions(-DWITHOUT_OPEN_MEMSTREAM)
    message(
        WARNING
        "funopen and fopencookie unavailable, open_memstream can not be implemented and conversion to JSON will not work properly!"
    )
else()
    target_sources(tinycbor PUBLIC
        src/open_memstream.c)
endif()

# examples
add_executable(simplereader examples/simplereader.c)
target_link_libraries(simplereader
    PRIVATE
        intel::tinycbor)

# tools
add_executable(cbordump tools/cbordump/cbordump.c)
target_link_libraries(cbordump
    PRIVATE
        intel::tinycbor)