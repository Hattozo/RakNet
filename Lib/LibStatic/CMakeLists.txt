cmake_minimum_required(VERSION 2.6)
project(RakNetLibStatic)

FILE(GLOB ALL_HEADER_SRCS ${RakNet_SOURCE_DIR}/Source/*.h)
FILE(GLOB ALL_CPP_SRCS ${RakNet_SOURCE_DIR}/Source/*.cpp)

include_directories( ${RAKNET_INTERNAL_INCLUDE_DIRS} ) 

add_library(RakNetLibStatic STATIC ${ALL_CPP_SRCS} ${ALL_HEADER_SRCS} readme.txt)

IF(WIN32 AND NOT UNIX)
	SET( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DWIN32 -D_RAKNET_LIB -D_CRT_NONSTDC_NO_DEPRECATE -D_CRT_SECURE_NO_DEPRECATE")
ENDIF(WIN32 AND NOT UNIX)

IF(WIN32 AND NOT UNIX)
	target_link_libraries (RakNetLibStatic ${RAKNET_LIBRARY_LIBS})
ELSE(WIN32 AND NOT UNIX)
	target_link_libraries (RakNetLibStatic ${RAKNET_LIBRARY_LIBS})
	INSTALL(TARGETS RakNetLibStatic DESTINATION ${RakNet_SOURCE_DIR}/Lib/RakNetLibStatic)
	INSTALL(FILES ${ALL_HEADER_SRCS} DESTINATION ${RakNet_SOURCE_DIR}/include/raknet)
ENDIF(WIN32 AND NOT UNIX)


