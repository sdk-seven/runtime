project('seven-rt', 'c',
  version: '0.12.1',
  license: 'Zlib',
  meson_version: '>=1.1.0',
  default_options: ['buildtype=debugoptimized', 'warning_level=2', 'c_std=c99'])

if not meson.is_subproject()
  subdir('meson/toolchain')
endif

subdir('tools')

sources_c = [
  'src/c/exit.c',
  'src/c/fini.c',
  'src/c/init.c',
  'src/c/start.c',
]

sources_rs = [
  'src/rust/start.c',
]

sources = [
  'src/gba/header.S',
  'src/gba/rt0.s',
]

lang = get_option('target_language')

if lang == 'c'
  sources += sources_c
elif lang == 'rust'
  sources += sources_rs
endif

lib = meson.current_source_dir() / 'lib'

link_args = ['-specs=' + lib / 'nocrt0.specs', '-L' + lib / 'ldscripts']

libdata = [
  'lib/ldscripts/gba.x',
  'lib/ldscripts/multiboot.mem',
  'lib/ldscripts/rom.mem',
  'lib/nocrt0.specs',
]

minrt = static_library(
  'minrt_rom',
  sources,
  c_args: ['-UMULTIBOOT'],
  link_depends: libdata)

minrt_mb = static_library(
  'minrt_mb',
  sources,
  c_args: ['-DMULTIBOOT'],
  link_depends: libdata)

minrt_dep = declare_dependency(
  link_with: minrt,
  link_args: link_args + ['-Trom.mem', '-Tgba.x'])

minrt_mb_dep = declare_dependency(
  link_with: minrt_mb,
  link_args: link_args + ['-Tmultiboot.mem', '-Tgba.x'])

meson.override_dependency('minrt', minrt_dep)
meson.override_dependency('minrt-multiboot', minrt_mb_dep)
