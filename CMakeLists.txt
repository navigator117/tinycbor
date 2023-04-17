cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

# project name
project(tinycbor-original)

# library name
zephyr_library_named(tinycbor-original)
zephyr_library_sources(PRIVATE
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
zephyr_library_include_directories(PUBLIC src)
zephyr_library_compile_options(-DCBOR_ENCODER_WRITER_CONTROL=-1 -DCBOR_PARSER_READER_CONTROL=-1)