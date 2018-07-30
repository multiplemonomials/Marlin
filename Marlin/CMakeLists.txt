cmake_minimum_required(VERSION 3.1)


# set AVR build properties
set(AVR_UPLOADTOOL avrdude)
set(AVR_PROGRAMMER arduino)
set(AVR_UPLOADTOOL_PORT COM3)
set(AVR_MCU atmega2560)
set(MCU_SPEED "16000000")

set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} -Wno-unused-variable)

# find core library
set(ARDUINO_CORE_LIBRARIES ${CMAKE_FIND_ROOT_PATH}/arduino_cores/mega/atmega2560/lib/libarduino-core.a)
include_directories(${CMAKE_FIND_ROOT_PATH}/arduino_cores/mega/atmega2560/include)
add_definitions(-DARDUINO=106)
	

set(MARLIN_SOURCES Marlin_main.cpp	
	MarlinSerial.cpp Sd2Card.cpp SdBaseFile.cpp SdFatUtil.cpp	
	SdFile.cpp SdVolume.cpp motion_control.cpp planner.cpp		
	stepper.cpp temperature.cpp cardreader.cpp ConfigurationStore.cpp 
	watchdog.cpp ultralcd.cpp digipot_mcp4451.cpp 
	vector_3.cpp qr_solve.cpp)
	

add_avr_executable(marlin ${MARLIN_SOURCES})
target_link_libraries(marlin.elf ${ARDUINO_CORE_LIBRARIES})