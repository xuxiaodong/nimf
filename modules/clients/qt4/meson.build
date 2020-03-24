qt4_gui = dependency('QtGui')
qt4_libdir = qt4_gui.get_pkgconfig_variable('libdir')
qt4_im_module_dir = qt4_libdir + '/qt4/plugins/inputmethods'

qt4 = import('qt4')
moc_files = qt4.preprocess(moc_sources : 'im-nimf-qt4.cpp')

cpp_args = ['-DG_LOG_DOMAIN="nimf"', '-DQT_NO_KEYWORDS']

deps = [qt4_gui,
    dependency('glib-2.0'),
    dependency('gobject-2.0'),
    dependency('gio-2.0')]

shared_library('qt4im_nimf', 
    sources : ['im-nimf-qt4.cpp', moc_files],
    include_directories: [libnimf_inc],
    cpp_args : cpp_args,
    cpp_std : 'c++11',
    link_with: libnimf,
    dependencies : deps,
    install : true,
    install_dir : qt4_im_module_dir)

install_data('org.nimf.clients.qt4.gschema.xml', 
    install_dir : get_option('datadir') + '/glib-2.0/schemas')
meson.add_install_script(meson.source_root() + '/meson_post_install.py')
