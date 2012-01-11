cmake_minimum_required(VERSION 2.6)

project(FacET)

set(FacET_SHARED_DIR share/FacET)
set(FacET_INCLUDE_DIR include)
set(FacET_LIBRARY_DIR lib)

install(DIRECTORY cascades DESTINATION ${FacET_SHARED_DIR}
  FILES_MATCHING PATTERN "*.xml")

set(FacET_CONFIGURATION_FILE facet.cfg)
configure_file(${FacET_CONFIGURATION_FILE}.in ${FacET_CONFIGURATION_FILE} @ONLY)
install(FILES ${FacET_BINARY_DIR}/${FacET_CONFIGURATION_FILE} DESTINATION ${FacET_SHARED_DIR})

set(FacET_PKGCONFIG_FILE facet.pc)
configure_file(${FacET_PKGCONFIG_FILE}.in ${FacET_PKGCONFIG_FILE} @ONLY)
install(FILES ${FacET_BINARY_DIR}/${FacET_PKGCONFIG_FILE} DESTINATION lib/pkgconfig)

add_subdirectory (src)
