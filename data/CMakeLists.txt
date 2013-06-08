ADD_SUBDIRECTORY(theme)

########### Add .desktop target ###############
CONFIGURE_FILE(
  "${CMAKE_CURRENT_SOURCE_DIR}/gogoo-panel-datetime.desktop.in"
  "${CMAKE_CURRENT_BINARY_DIR}/gogoo-panel-datetime.desktop"
  IMMEDIATE @ONLY)
INSTALL(FILES ${CMAKE_CURRENT_BINARY_DIR}/gogoo-panel-datetime.desktop DESTINATION share/mutter-neetbook/panels)

