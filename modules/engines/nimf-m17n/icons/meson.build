icon_theme_dir = '@0@/icons/hicolor'.format(get_option('datadir'))
rsvg_convert = find_program('rsvg-convert', 'rsvg')
assert(rsvg_convert.found(),
    'rsvg-convert or rsvg is not found, please install librsvg2-bin')

foreach lang : langs
    basename = 'nimf-m17n-@0@'.format(lang)
    icon = 'scalable/' + basename + '.svg'
    scaled_icon = '@0@.png'.format(basename)
    install_data(icon, install_dir : icon_theme_dir + '/scalable/status')
    foreach p : ['16', '22', '24', '32', '48', '96', '256']
        outdir = 'resized/@0@/'.format(p)
        run_command('mkdir', '-p', outdir)
        run_command(rsvg_convert, '-w', p, '-h', p, '-o', outdir + scaled_icon, icon)
        install_data(outdir + scaled_icon,
            install_dir : icon_theme_dir + '/@0@x@1@/status'.format(p, p))
    endforeach
endforeach