set(DEBUG "-O2")
set(INCLUDE "-I.")
set(CMAKE_C_FLAGS "${DEBUG} -Wall -Winline ${INCLUDE} -pipe")
set(DYN_VERS_MAJ 2)
set(DYN_VERS_MIN 0)
set(GPIO gpio)

include_directories(../wiringPi)
include_directories(../devLib)

set(gpio_Sources
        gpio.c
        extensions.c
        readall.c
        pins.c
        )

set(gpio_Headers
        extensions.h
        )

set(gpio_ManPages
        gpio.1
        )


add_executable(${GPIO} ${gpio_Sources} ${gpio_Headers})
target_link_libraries(${GPIO} PUBLIC "wiringPi")
target_link_libraries(${GPIO} PUBLIC "wiringPiDev")
target_link_libraries(${GPIO} PUBLIC pthread)
target_link_libraries(${GPIO} PUBLIC m)

install(TARGETS ${GPIO}
        RUNTIME DESTINATION bin
        PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
)

install(FILES ${gpio_ManPages}
        DESTINATION man/man1
        )
