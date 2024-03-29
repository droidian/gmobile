gm_deps = [
  epoll_dep,
  gio_dep,
  glib_dep,
  json_glib_dep,
  cc.find_library('m', required: false),
  cc.find_library('rt', required: false),
]

gm_public_sources = files(
  'gmobile.h',
  'gm-cutout.c',
  'gm-cutout.h',
  'gm-device-info.c',
  'gm-device-info.h',
  'gm-device-tree.c',
  'gm-device-tree.h',
  'gm-display-panel.c',
  'gm-display-panel.h',
  'gm-error.c',
  'gm-error.h',
  'gm-main.c',
  'gm-main.h',
  'gm-rect.c',
  'gm-rect.h',
  'gm-svg-path.c',
  'gm-svg-path.h',
  'gm-timeout.c',
  'gm-timeout.h',
  'gm-util.c',
  'gm-util.h',
)

gm_sources = [
  gm_public_sources,
  gm_resources,
]

gm_c_args = [
  '-DG_LOG_DOMAIN="gmobile"',
]

gm_lib = both_libraries(
  'gmobile',
  gm_sources,
  include_directories: root_inc,
  c_args: gm_c_args,
  dependencies: gm_deps,
  # Will switch to '0' for the first release
  soversion: '0c',
  install: true)

gmobile_dep = declare_dependency(
  include_directories: [root_inc, include_directories('.')],
  dependencies: gm_deps,
  link_with: gm_lib.get_static_lib())

gmobile_shared_dep = declare_dependency(
  include_directories: [root_inc, include_directories('.')],
  dependencies: gm_deps,
  link_with: gm_lib.get_shared_lib())

pkgconfig = import('pkgconfig')
pkgconfig.generate(
        gm_lib,
	description: 'Functions useful in mobile related, glib based projects',
	url: 'https://world.pages.gitlab.gnome.org/Phosh/gmobile/',
)

if get_option('gtk_doc')
  gmobile_gir_extra_args = [
    '--c-include=gmobile.h',
    '-L@0@'.format(meson.current_build_dir()),
    '--quiet',
    '-DGMOBILE_USE_UNSTABLE_API',
   ]

  gmobile_gir = gnome.generate_gir(gm_lib,
                 sources: gm_sources,
               nsversion: '0',
               namespace: 'Gm',
         export_packages: 'gmobile-0',
           symbol_prefix: 'gm',
       identifier_prefix: 'Gm',
                includes: ['Gio-2.0'],
                 install: false,
              extra_args: gmobile_gir_extra_args,
   )
endif
