cmake_minimum_required(VERSION 3.13)

set(CMAKE_INCLUDE_DIRECTORIES_PROJECT_BEFORE ON)

project(orumcek)


if (WIN32)
    OPTION(WITH_WIN32_GUI "Enable Gui build (default off)")
endif (WIN32)

include(ConfigureChecks.cmake)

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    # using Clang

    set( CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -std=c++11 -O3 -march=native -mtune=native -pedantic -stdlib=libc++")

elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    # using G++

    if (CMAKE_CXX_COMPILER_VERSION VERSION_LESS 5.1)
        message(FATAL_ERROR "G++ 5.1 or higher required")
    endif()

    set( CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -std=c++11 -O3 -march=native -mtune=native -pedantic -Wno-variadic-macros" )

elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    # using Visual Studio

    if (CMAKE_CXX_COMPILER_VERSION VERSION_LESS 19.0)
        message(FATAL_ERROR "Visual Studio 2015 or higher required")
    endif()


    # DEBUG compiler flags:
    #	/Zi create debugging information PDB file
    #	/Od disable optimizations
    # 	/Oy- do not suppress frame pointers (recommended for debugging)
    #	/MTd use statically linked, thread-safe, debug CRT libs (Magic Builder set this flag when build)
    #
    # RELEASE compiler flags:
    #	/MT use statically linked, thread-safe CRT libs (Magic Builder set this flag when build)
    # 	/GS- no Buffer Security Check
    #
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /Zi /Od /Oy-")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /Zi")

    # Explaining of linker flags and why enable pdb with debug info for Release build is on:
    #  https://www.wintellect.com/correctly-creating-native-c-release-build-pdbs
    set(CMAKE_EXE_LINKER_FLAGS_RELEASE "${CMAKE_EXE_LINKER_FLAGS_RELEASE} /DEBUG /OPT:REF /OPT:ICF")
endif()


subdirs(src)