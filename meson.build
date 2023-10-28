project('seven-rt', 'c',
  version: '0.10.1',
  license: 'Zlib',
  meson_version: '>=1.1.0',
  default_options: ['buildtype=debugoptimized', 'warning_level=2', 'c_std=c99'])

if not meson.is_subproject()
  subdir('meson/toolchain')
endif

subdir('tools')
subdir('rt')
