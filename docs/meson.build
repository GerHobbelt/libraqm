gtkdoc = find_program('gtkdoc-scan', required: false)

if not gtkdoc.found()
  error('MESON_SKIP_TEST gtkdoc not found.')
endif

version_xml = configure_file(input : 'version.xml.in',
                             output : 'version.xml',
                             configuration : conf)

gnome = import('gnome')
gnome.gtkdoc(
  'raqm',
  main_xml : 'raqm-docs.xml',
  src_dir : join_paths(meson.source_root(), 'src'),
  content_files : [version_xml],
  mkdb_args : ['--xml-mode', '--output-format=xml'],
  install : true,
)