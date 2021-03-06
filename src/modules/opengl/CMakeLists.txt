add_library(mltopengl MODULE
  consumer_xgl.c
  factory.c
  filter_glsl_manager.cpp
  filter_movit_blur.cpp
  filter_movit_convert.cpp
  filter_movit_crop.cpp
  filter_movit_deconvolution_sharpen.cpp
  filter_movit_diffusion.cpp
  filter_movit_flip.cpp
  filter_movit_glow.cpp
  filter_movit_lift_gamma_gain.cpp
  filter_movit_mirror.cpp
  filter_movit_opacity.cpp
  filter_movit_rect.cpp
  filter_movit_resample.cpp
  filter_movit_resize.cpp
  filter_movit_saturation.cpp
  filter_movit_vignette.cpp
  filter_movit_white_balance.cpp
  mlt_movit_input.cpp
  transition_movit_luma.cpp
  transition_movit_mix.cpp
  transition_movit_overlay.cpp
)

target_link_libraries(mltopengl m Threads::Threads mlt mlt++ OpenGL::GL PkgConfig::movit)

if(UNIX AND NOT APPLE)
  target_link_libraries(mltopengl X11::X11)
endif()

pkg_get_variable(SHADERDIR movit shaderdir)
target_compile_definitions(mltopengl PRIVATE SHADERDIR="${SHADERDIR}")

# Create module in parent directory, for the benefit of "source setenv".
set_target_properties(mltopengl PROPERTIES LIBRARY_OUTPUT_DIRECTORY ..)

install(TARGETS mltopengl LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}/mlt)

install(FILES
  filter_movit_blur.yml
  filter_movit_deconvolution_sharpen.yml
  filter_movit_diffusion.yml
  filter_movit_flip.yml
  filter_movit_glow.yml
  filter_movit_lift_gamma_gain.yml
  filter_movit_mirror.yml
  filter_movit_opacity.yml
  filter_movit_rect.yml
  filter_movit_saturation.yml
  filter_movit_vignette.yml
  filter_movit_white_balance.yml
  transition_movit_luma.yml
  transition_movit_mix.yml
  transition_movit_overlay.yml
  DESTINATION ${CMAKE_INSTALL_DATADIR}/mlt/opengl
)
