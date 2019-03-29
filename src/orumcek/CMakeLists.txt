

set(ORUMCEK_SOURCES
        main.cpp)
find_package(Boost 1.65.1 COMPONENTS system filesystem )

include_directories(${Boost_INCLUDE_DIRS})
link_directories(${Boost_LIBRARY_DIR})
add_executable(Orumcek ${ORUMCEK_SOURCES})
target_link_libraries(Orumcek ${Boost_LIBRARIES})
install(TARGETS Orumcek DESTINATION ${SBINDIR})