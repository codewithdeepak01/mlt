add_library(mltxml MODULE
  common.c
  consumer_xml.c
  factory.c
  producer_xml.c
)

target_link_libraries(mltxml mlt Threads::Threads PkgConfig::xml)

# Create module in parent directory, for the benefit of "source setenv".
set_target_properties(mltxml PROPERTIES LIBRARY_OUTPUT_DIRECTORY ..)

install(TARGETS mltxml LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}/mlt)

install(FILES
  consumer_xml.yml
  producer_xml-nogl.yml
  producer_xml-string.yml
  producer_xml.yml
  mlt-xml.dtd
  DESTINATION ${CMAKE_INSTALL_DATADIR}/mlt/xml
)
