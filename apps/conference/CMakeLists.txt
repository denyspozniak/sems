set (conference_SRCS
Conference.cpp
)

set (conference_audio_files
beep.wav
first_participant.wav
)

INCLUDE_DIRECTORIES(${LIBEVENT2_INCLUDE_DIR})

IF(FLITE_FOUND AND ZRTP_FOUND)
	INCLUDE_DIRECTORIES(${FLITE_INCLUDE_DIR}/flite)
	ADD_DEFINITIONS(-DWITH_SAS_TTS)
	SET(sems_module_libs ${sems_module_libs} flite_cmu_us_kal flite_usenglish flite_cmulex ${FLITE_LIBRARIES})
ENDIF(FLITE_FOUND AND ZRTP_FOUND)

IF(MYSQLPP_FOUND)
	INCLUDE_DIRECTORIES(/usr/include/mysql)
	INCLUDE_DIRECTORIES(${MYSQLPP_INCLUDE_DIR}/mysql++)
	ADD_DEFINITIONS(-DUSE_MYSQL)
	SET(sems_module_libs ${sems_module_libs} ${MYSQLPP_LIBRARIES})
ENDIF(MYSQLPP_FOUND)

SET(sems_module_name conference)
INCLUDE(${CMAKE_SOURCE_DIR}/cmake/module.rules.txt)
