set(FacET_SRC 
  components.cpp
  face_regions.cpp
  facet.cpp
  FastMatchTemplate.cpp
  image_processing.cpp
  )

set(FacET_HDR
  facet.h
  FastMatchTemplate.h
)
foreach(IN ${FacET_HDR})
  configure_file(${IN}.in ${IN} @ONLY)
  set(FacET_HDR_TMP ${FacET_HDR_TMP} ${FacET_BINARY_DIR}/src/${IN})
endforeach(IN)
include_directories (${FacET_BINARY_DIR}/src)
set(FacET_HDR ${FacET_HDR_TMP})
unset(FacET_HDR_TMP)
install(FILES ${FacET_HDR} DESTINATION ${FacET_INCLUDE_DIR})

find_package (OpenCV REQUIRED)

include_directories (${OpenCV_INCLUDE_DIRS})
link_directories(${OpenCV_LINK_DIRECTORIES})

add_library(facetShared SHARED ${FacET_SRC})
target_link_libraries(facetShared ${OpenCV_LIBRARIES})
set_target_properties (facetShared PROPERTIES
  VERSION 2.2.1
  SOVERSION 2.2.1
  OUTPUT_NAME facet
  )
install(TARGETS facetShared DESTINATION lib)

add_library(facetStatic STATIC ${FacET_SRC})
target_link_libraries(facetStatic ${OpenCV_LIBRARIES})
set_target_properties (facetStatic PROPERTIES
  VERSION 2.2.1
  SOVERSION 2.2.1
  OUTPUT_NAME facet
  )
install(TARGETS facetStatic DESTINATION ${FacET_LIBRARY_DIR})

#instalacja hederow
