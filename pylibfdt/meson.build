swig_include_dir = meson.project_source_root() / 'libfdt'

pylibfdt_swig = custom_target(
  'libfdt.py',
  input: 'libfdt.i',
  output: ['libfdt.py', 'libfdt_wrap.c'],
  command: [swig, '-python', '-I@0@'.format(swig_include_dir), '-o', '@OUTPUT1@', '@INPUT0@'],
  install: true,
  install_dir: [py.get_install_dir(pure: false), false],
)

pylibfdt = py.extension_module(
  '_libfdt',
  pylibfdt_swig[1],
  c_args: ['-DPY_SSIZE_T_CLEAN', '-Wno-redundant-decls', '-Wno-cast-qual'],
  dependencies: [libfdt_dep, py.dependency()],
  override_options: 'werror=false',
  install: true,
)
