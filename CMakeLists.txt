cmake_minimum_required(VERSION 3.5)
project(WiringNP)

set(CMAKE_CXX_STANDARD 11)
SET(CMAKE_SYSTEM_NAME Linux)
SET(CMAKE_SYSTEM_VERSION 1)
SET(CXX_FLAGS "${CXX_FLAGS} -fpermissive")

set(CMAKE_INSTALL_PREFIX "../debian-package/wiringNP/pkgsrc/usr/local" )

add_subdirectory(wiringPi)
add_subdirectory(devLib)
add_subdirectory(gpio)

add_custom_target(BUILD_ALL DEPENDS "staticwiringPi" "wiringPi" "staticwiringPiDev" "wiringPiDev" gpio)
