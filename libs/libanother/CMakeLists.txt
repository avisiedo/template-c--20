# CMakeLists.txt libanother

add_library(another src/another_delegate.cpp)
target_include_directories(another PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/libanother)

# Si necesitas enlazar las librerías entre sí, puedes hacerlo aquí
# target_link_libraries(libanother libstdc++)

