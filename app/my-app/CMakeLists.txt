# CMakeLists.txt my-app

set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREAD ON)
set(Boost_USE_STATIC_RUNTIME ON)
find_package(Boost CONFIG)
# find_package(Boost 1.89.0 COMPONENTS filesystem regex)

# Apply conditionally extra arguments to the compiler
set_directory_properties(PROPERTIES
    COMPILE_OPTIONS "$<$<OR:$<CXX_COMPILER_ID:GNU>,$<CXX_COMPILER_ID:Clang>>:-Wall;-Wextra>;$<$<CXX_COMPILER_ID:MSVC>:/W4>"
)

 if (Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
    add_executable(my-app src/main.cpp)
    target_include_directories(my-app PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
 endif()

set_target_properties(my-app PROPERTIES
    POSITION_INDEPENDENT_CODE ON
    CXX_VISIBILITY_PRESET hidden
)

target_compile_definitions(my-app PRIVATE
    $<$<PLATFORM_ID:Windows>:IMAGELITE_WINDOWS>
    $<$<PLATFORM_ID:Linux>:IMAGELITE_LINUX>
    $<$<PLATFORM_ID:Darwin>:IMAGELITE_MACOS>
)

target_compile_options(my-app PRIVATE
    # Extra strict flags for our application code
    $<$<CXX_COMPILER_ID:GNU>:-Wall -Wextra -Wpedantic -Wconversion -Wshadow>
    $<$<CXX_COMPILER_ID:Clang>:-Wall -Wextra -Wpedantic -Wconversion -Wshadow>
    $<$<CXX_COMPILER_ID:MSVC>:/W4 /WX>
)

target_compile_options(my-app PRIVATE
    $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:GNU>>:-Wpedantic -g>
    $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:Clang>>:-Wpedantic -g>
    $<$<AND:$<CONFIG:Debug>,$<CXX_COMPILER_ID:MSVC>>:/Zi /Od>
)

target_compile_options(my-app PRIVATE
    $<$<AND:$<CONFIG:Release>,$<OR:$<CXX_COMPILER_ID:GNU>,$<CXX_COMPILER_ID:Clang>>>:-O3>
    $<$<AND:$<CONFIG:Release>,$<CXX_COMPILER_ID:MSVC>>:/O2>
)

target_compile_definitions(my-app PRIVATE
    $<$<CONFIG:Debug>:MY_APP_DEBUG>
    $<$<CONFIG:Debug>:MY_APP_ENABLE_LOGGING>
    $<$<CONFIG:Release>:MY_APP_RELEASE>
)

set_target_properties(my-app PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/bin/debug"
    RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/release"
)

# target_link_libraries(otra_libreria mi_libreria)

