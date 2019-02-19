set(DEBUG "-O2")
set(DEFS "-D_GNU_SOURCE")
set(INCLUDE "-I.")
set(CMAKE_C_FLAGS "${DEBUG} ${DEFS} -Wformat=2 -Wall -Winline ${INCLUDE} -pipe -fPIC -Wpointer-to-int-cast")
set(DYN_VERS_MAJ 2)
set(DYN_VERS_MIN 0)
set(VERSION ${DYN_VERS_MAJ}.${DYN_VERS_MIN})
set(WIRING_PI wiringPi)


set(wiringPi_Sources
        wiringPi.c
        wiringSerial.c
        wiringShift.c
        piHiPri.c
        piThread.c
        wiringPiSPI.c
        wiringPiI2C.c
        softPwm.c
        softTone.c
        softServo.c
        mcp23008.c
        mcp23016.c
        mcp23017.c
        mcp23s08.c
        mcp23s17.c
        sr595.c
        pcf8574.c
        pcf8591.c
        mcp3002.c
        mcp3004.c
        mcp4802.c
        mcp3422.c
        max31855.c
        max5322.c
        sn3218.c
        drcSerial.c
        boardtype_friendlyelec.c
        )

set(wiringPi_Headers
        wiringPi.h
        wiringSerial.h
        wiringShift.h
        softPwm.h
        softTone.h
        softServo.h
        wiringPiSPI.h
        wiringPiI2C.h
        drcSerial.h
        mcp23008.h
        mcp23016.h
        mcp23s08.h
        mcp23s17.h
        max31855.h
        max5322.h
        mcp3002.h
        mcp3004.h
        mcp4802.h
        mcp3422.h
        sr595.h
        pcf8574.h
        pcf8591.h
        sn3218.h
        boardtype_friendlyelec.h
        )

add_library("static${WIRING_PI}" STATIC ${wiringPi_Headers} ${wiringPi_Sources})
add_library(${WIRING_PI} SHARED ${wiringPi_Headers} ${wiringPi_Sources})

install(PROGRAMS "${CMAKE_CURRENT_BINARY_DIR}/libstatic${WIRING_PI}.a"
        DESTINATION lib
        RENAME "lib${WIRING_PI}.a"
        )
install(PROGRAMS "${CMAKE_CURRENT_BINARY_DIR}/lib${WIRING_PI}.so"
        DESTINATION lib
        RENAME "lib${WIRING_PI}.so.${VERSION}"
        )
install(FILES ${wiringPi_Headers}
        DESTINATION include
        )
