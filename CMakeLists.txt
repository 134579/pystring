cmake_minimum_required(VERSION 3.2)
project(pystring CXX)
option(PYSTRING_BUILD_TESTS "build tests." OFF)
add_library(pystring STATIC
    pystring.cpp
    pystring.h
)

target_include_directories(pystring PUBLIC .)
add_library(pystring::pystring ALIAS pystring)

if(PYSTRING_BUILD_TESTS)
    add_executable (pystring_test test.cpp)
    TARGET_LINK_LIBRARIES (pystring_test pystring)

    enable_testing()
    add_test(NAME PyStringTest COMMAND pystring_test)

    include(GNUInstallDirs)

    install(TARGETS pystring
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    )
endif()