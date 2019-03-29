

set(ORUMCEK_SOURCES
        main.cpp
)


add_executable(orumcek ${ORUMCEK_SOURCES})

install(TARGETS orumcek DESTINATION ${SBINDIR})