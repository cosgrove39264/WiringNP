set(DEBUG "-O2")
set(INCLUDE "-I.")
set(CMAKE_C_FLAGS "${DEBUG} -Wformat=2 -Wall -Winline ${INCLUDE} -pipe -fPIC")
set(DYN_VERS_MAJ 2)
set(DYN_VERS_MIN 0)
set(VERSION ${DYN_VERS_MAJ}.${DYN_VERS_MIN})
set(WIRING_PI_DEV wiringPiDev)

set(wiringPiDev_Sources
        ds1302.c
        maxdetect.c
        piNes.c
		gertboard.c
        piFace.c
		lcd128x64.c
        lcd.c
		piGlow.c
        )

set(wiringPiDev_Headers
        	ds1302.h
	        maxdetect.h
	        piNes.h
	        gertboard.h
	        piFace.h
	        lcd128x64.h
	        lcd.h
	        piGlow.h
        )

add_library("static${WIRING_PI_DEV}" STATIC ${wiringPiDev_Headers} ${wiringPiDev_Sources})
add_library(${WIRING_PI_DEV} SHARED ${wiringPiDev_Headers} ${wiringPiDev_Sources})

install(PROGRAMS "${CMAKE_CURRENT_BINARY_DIR}/libstatic${WIRING_PI_DEV}.a"
        DESTINATION lib
        RENAME "lib${WIRING_PI_DEV}.a"
        )
install(PROGRAMS "${CMAKE_CURRENT_BINARY_DIR}/lib${WIRING_PI_DEV}.so"
        DESTINATION lib
        RENAME "lib${WIRING_PI_DEV}.so.${VERSION}"
        )
install(FILES ${wiringPiDev_Headers}
        DESTINATION include
        )
