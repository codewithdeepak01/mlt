set_source_files_properties(../mlt.i PROPERTIES USE_TARGET_INCLUDE_DIRECTORIES ON CPLUSPLUS ON)

swig_add_library(mltphp LANGUAGE php SOURCES ../mlt.i)
target_link_libraries(mltphp mlt mlt++ PHP::Extension)
set_target_properties(mltphp PROPERTIES OUTPUT_NAME "mlt")

if(PHP_EXTENSION_DIR)
  string(REGEX MATCH "lib.*" PHP_EXTENSION_INSTALL_DIR ${PHP_EXTENSION_DIR})
  install(TARGETS mltphp DESTINATION ${PHP_EXTENSION_INSTALL_DIR})
  install(FILES ${CMAKE_CURRENT_BINARY_DIR}/mlt.php DESTINATION ${PHP_EXTENSION_INSTALL_DIR})
endif()
