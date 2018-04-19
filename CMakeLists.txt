cmake_minimum_required(VERSION 3.1)

project(RHash)

file(GLOB rhash_headers *.h)
file(GLOB rhash_sources *.c)

# Setup the library sources, removing any test files
set(librhash_path ${CMAKE_CURRENT_SOURCE_DIR}/librhash)
file(GLOB librhash_headers ${librhash_path}/*.h)
file(GLOB librhash_sources ${librhash_path}/*.c)
list(REMOVE_ITEM librhash_sources ${librhash_path}/test_hashes.c)

add_library(rhash-library ${librhash_sources} ${librhash_headers})

if (NOT RHASH_LIBRARY_ONLY)
    add_executable(rhash-command  ${rhash_headers} ${rhash_sources})
    set_target_properties(rhash-command PROPERTIES OUTPUT_NAME rhash)
    target_link_libraries(rhash-command rhash-library)
endif ()