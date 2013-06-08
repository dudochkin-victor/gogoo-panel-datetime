SET(VERSION_MAJOR 0)
SET(VERSION_MINOR 0)
SET(VERSION_PATCH 0)

INCLUDE_DIRECTORIES(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}/common
    ${GWEATHER_INCLUDE_DIRS}
    ${GCONF_INCLUDE_DIRS}
    ${JANA_INCLUDE_DIRS}
    ${PENGE_INCLUDE_DIRS}
    ${MPL_INCLUDE_DIRS}
#    ${SQLITE3_INCLUDE_DIRS}
    )


SET (PROGRAMS gogoo-panel-datetime)

ADD_DEFINITIONS(-DLOCALEDIR="${LOCALEDIR}")
ADD_DEFINITIONS(-DMX_CACHE="${DATADIR}/mx.cache")
ADD_DEFINITIONS(-DTHEMEDIR="${PKG_DATADIR}/${PROGRAMS}/theme")
ADD_DEFINITIONS(-DGETTEXT_PACKAGE="${GETTEXT_PACKAGE}")
ADD_DEFINITIONS(-DDATADIR="${PKG_DATADIR}/${PROGRAMS}")


SET(PROGRAM_SRCS
	meego-panel-date-time.c	
	mnp-world-clock.c	
	mnp-world-clock.h	
	mnp-utils.c 		
	mnp-utils.h		
	mnp-button-item.c	
	mnp-button-item.h	
	system-timezone.c	
	system-timezone.h	
	mnp-clock-tile.c	
	mnp-clock-tile.h	
	mnp-clock-area.c	
	mnp-clock-area.h	
	mnp-datetime.c		
	mnp-datetime.h		
	mnp-shell.c		
	mnp-shell.h
    )

SET(PROGRAM_HEADERS
    )

ADD_EXECUTABLE(${PROGRAMS} ${PROGRAM_SRCS} ${PROGRAM_HEADERS})

   
TARGET_LINK_LIBRARIES(${PROGRAMS}
    ${GWEATHER_LIBRARIES}
    ${MPL_LIBRARIES}
    ${GCONF_LIBRARIES}
    ${JANA_LIBRARIES}
    ${PENGE_LIBRARIES}
    )

INSTALL(TARGETS ${PROGRAMS} RUNTIME DESTINATION ${PKG_LIBEXECDIR})

########### Add .desktop target ###############
CONFIGURE_FILE(
  "${CMAKE_CURRENT_SOURCE_DIR}/date-time.schemas.in"
  "${CMAKE_CURRENT_BINARY_DIR}/date-time.schemas"
  IMMEDIATE @ONLY)
INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/date-time.schemas DESTINATION /etc/gconf)

########### Add .service target ###############
CONFIGURE_FILE(
  "${CMAKE_CURRENT_SOURCE_DIR}/com.meego.UX.Shell.Panels.datetime.service.in"
  "${CMAKE_CURRENT_BINARY_DIR}/com.meego.UX.Shell.Panels.datetime.service"
  IMMEDIATE @ONLY)
INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/com.meego.UX.Shell.Panels.datetime.service DESTINATION share/dbus-1/services)


