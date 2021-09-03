cc = meson.get_compiler('c')

config_h = configuration_data()
if freetype.type_name() == 'internal' or \
  cc.has_function('FT_Get_Transform', dependencies : freetype)
  config_h.set('HAVE_FT_GET_TRANSFORM', 1)
endif
if harfbuzz.type_name() == 'internal' or \
  cc.has_function('hb_buffer_set_invisible_glyph', dependencies : harfbuzz)
  config_h.set('HAVE_HB_BUFFER_SET_INVISIBLE_GLYPH', 1)
endif
if harfbuzz.type_name() == 'internal' or \
  cc.has_header_symbol('hb.h', 'HB_BUFFER_FLAG_REMOVE_DEFAULT_IGNORABLES', dependencies : harfbuzz)
  config_h.set('HAVE_DECL_HB_BUFFER_FLAG_REMOVE_DEFAULT_IGNORABLES', 1)
endif
if cc.get_argument_syntax() == 'msvc'
  library_type = get_option('default_library')
  if library_type == 'shared' or library_type == 'both'
    config_h.set('RAQM_API', '__declspec (dllexport)')
  endif
endif
configure_file(output : 'config.h', configuration : config_h)

version_h = configuration_data()
version_h.set('RAQM_VERSION_MAJOR', raqm_version[0].to_int())
version_h.set('RAQM_VERSION_MINOR', raqm_version[1].to_int())
version_h.set('RAQM_VERSION_MICRO', raqm_version[2].to_int())
version_h.set('RAQM_VERSION', meson.project_version())

configure_file(
  input : 'raqm-version.h.in',
  output : 'raqm-version.h',
  configuration : version_h)

libraqm = library(
  'raqm',
  'raqm.c',
  'raqm.h',
  dependencies : deps,
  c_args : ['-DHAVE_CONFIG_H'],
  install : true,
)

libraqm_test = static_library(
  'raqm-test',
  'raqm.c',
  'raqm.h',
  dependencies : deps,
  c_args : ['-DRAQM_TESTING', '-DHAVE_CONFIG_H'],
  install : false,
)
