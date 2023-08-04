setup_py = find_program('../setup.py')
setup_py = [setup_py, '--quiet', '--top-builddir', meson.project_build_root()]

libfdt_i = configure_file(input: 'libfdt.i', output: '@PLAINNAME@', copy: true)

pylibfdt = custom_target(
  'pylibfdt',
  input: libfdt_i,
  depends: libfdt,
  output: '_libfdt.so',
  command: [setup_py, 'build_ext'],
  build_by_default: true,
)

meson.add_install_script(setup_py, 'install', '--prefix=' + get_option('prefix'), '--root=$DESTDIR')
