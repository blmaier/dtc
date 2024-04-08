py = import('python')
py = py.find_installation(required: get_option('python'))
swig = find_program('swig', required: get_option('python'))
pylibfdt_enabled = not meson.is_cross_build() and py.found() and swig.found()

if pylibfdt_enabled
  # setup_py = find_program('../setup.py')
  # setup_py = [setup_py, '--quiet', '--top-builddir', meson.project_build_root()]

  swig_include_dir = meson.project_source_root() / 'libfdt'

  pylibfdt_swig = custom_target(
    'libfdt_wrap.py',
    input: 'libfdt.i',
    output: ['libfdt.py', 'libfdt_wrap.c'],
    command: [swig, '-python', '-I@0@'.format(swig_include_dir), '-o', '@OUTPUT1@', '@INPUT0@'],
    install: true,
    install_dir: [py.get_install_dir(pure: false), false],
  )

  pylibfdt = py.extension_module(
    '_libfdt',
    pylibfdt_swig[1],
    c_args: '-DPY_SSIZE_T_CLEAN',
    dependencies: [libfdt_dep, py.dependency()],
    override_options: 'werror=false',
    install: true,
  )
  # install_dir: py.get_install_dir(pure: false)

  # meson.add_install_script(setup_py, 'install', '--prefix=' + get_option('prefix'), '--root=$DESTDIR')
endif
