#
# project: fips-xxhash
#

if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup(PROJECT fips-xxhash)
endif()

fips_begin_lib(xxhash)
    include_directories(xxHash)
    fips_dir(xxHash)
    fips_files(
        xxhash.h
        xxhash.c
    )
fips_end_lib()

if (NOT FIPS_IMPORT)
    fips_begin_app(xxhsum cmdline)
        fips_dir(xxHash)
        fips_files(
            xxhsum.c
        )
        fips_deps(xxhash)
    fips_end_app()
    fips_finish()
endif()
