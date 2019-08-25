# vim: set ai ts=4 expandtab:
# ::=========================================================================::

cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(lmdb VERSION 0.9.23)
find_package(Threads REQUIRED)
SET(HEADERS_LMDB
    lmdb.h
    midl.h
    lmdbpp.h
)

SET(SOURCES_LMDB
    mdb.c
    midl.c
)

SET(LMDB_STATIC_LIB lmdb)

add_definitions("-DMDB_FDATASYNC_WORKS")

add_library(${LMDB_STATIC_LIB} STATIC ${HEADERS_LMDB} ${SOURCES_LMDB})

message(STATUS "LMDB checking HAVE_FLAG_STD_CXX17...")
if (MSVC)
    check_cxx_compiler_flag(/std:c++17 HAVE_FLAG_STD_CXX17)
else()
    check_cxx_compiler_flag(-std=c++17 HAVE_FLAG_STD_CXX17)
endif()