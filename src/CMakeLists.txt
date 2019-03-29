include_directories(${CMAKE_BINARY_DIR} ${CMAKE_SOURCE_DIR}/src)

link_directories(
        ${CMAKE_BINARY_DIR}/src/common
        ${CMAKE_BINARY_DIR}/src/config
        ${CMAKE_BINARY_DIR}/src/network
        ${CMAKE_BINARY_DIR}/src/orumcek
)

add_subdirectory(orumcek)