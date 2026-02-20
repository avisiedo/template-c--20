# Inspired from GPT-4o mini
cmake_minimum_required(VERSION 3.10)
project(myApp
    VERSION 0.1.0
    DESCRIPTION "TODO Template for C++ library/application build with cmake"
    LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

set(USE_BOOST ON)
set(USE_QT OFF)

# ------------------ Platform detection ----------------------------------------
message(STATUS "Detecting platform...")
if(WIN32)
    message(STATUS "Platform: Windows")
elseif(APPLE)
    message(STATUS "Platform: macOS, iOS, tvOS, visionOS or watchOS")
elseif(UNIX AND NOT APPLE)
    message(STATUS "Platform: Linux")
else()
    message(STATUS "Platform: Unknown")
endif()

# ---------------------------- FetchContent ------------------------------------
# ------- FetchContent with Boost
# https://discourse.cmake.org/t/fetchcontent-with-boost/6596
# https://cmake.org/cmake/help/latest/module/FetchContent.html
include(FetchContent)

if (USE_BOOST)
    # Installation:
    #   Fedora: run0 dnf install boost-devel
    find_package(Boost
        CONFIG
        REQUIRED
    )
endif()


# Add subdirectories (libs and app)
add_subdirectory(libs)
add_subdirectory(app)

string(COMPARE EQUAL
    "${CMAKE_SOURCE_DIR}"
    "${CMAKE_CURRENT_SOURCE_DIR}"
    is_top_level)

include(GNUInstallDirs)

# ---------------------------------- TESTS -------------------------------------

# TODO Integrate googletest

# https://google.github.io/googletest/quickstart-cmake.html

# Google tests configuration
enable_testing()

# Define the path to Google Test
# set(GTEST_DIR "${CMAKE_CURRENT_SOURCE_DIR}/third_party/googletest")
# set(GOOGLETEST_VERSION "1.17.0")

# Add Google Test to the build
# add_subdirectory(${GTEST_DIR} ${CMAKE_CURRENT_BINARY_DIR}/googletest)

add_subdirectory(tests)

# ------------------------------ Custom targets --------------------------------

add_custom_target(run
    COMMAND my-app
    DEPENDS my-app
    WORKING_DIRECTORY ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}
    COMMENT "Running the CLI my-app"
)

