cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

# project name
project(tinycbor-original)

# library name
zephyr_library_named(tinycbor-original)
zephyr_library_sources(PRIVATE
    ${ZEPHYR_CURRENT_MODULE_DIR}/src/cborerrorstrings.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborencoder.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborencoder_close_container_checked.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborencoder_float.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborparser.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborparser_float.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborpretty.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborparser_dup_string.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborpretty_stdio.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cbortojson.c
	${ZEPHYR_CURRENT_MODULE_DIR}/src/cborvalidation.c)
zephyr_library_include_directories(PUBLIC
	${ZEPHYR_CURRENT_MODULE_DIR}/src)
zephyr_library_compile_options(-DCBOR_ENCODER_WRITER_CONTROL=-1 -DCBOR_PARSER_READER_CONTROL=-1)