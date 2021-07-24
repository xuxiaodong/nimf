gsettings_SCHEMAS = org.nimf.clients.gtk.gschema.xml
@GSETTINGS_RULES@

AM_CFLAGS = \
	$(EXTRA_CFLAGS) \
	-I$(top_srcdir)/libnimf \
	-DG_LOG_DOMAIN=\"nimf\"

# for gtk3

gtk3_im_moduledir = $(GTK3_LIBDIR)/gtk-3.0/$(GTK3_BINARY_VERSION)/immodules
gtk3_im_module_LTLIBRARIES = im-nimf-gtk3.la

im_nimf_gtk3_la_SOURCES  = im-nimf.c
im_nimf_gtk3_la_CFLAGS   = $(IM_NIMF_GTK3_DEPS_CFLAGS) $(AM_CFLAGS)
im_nimf_gtk3_la_LDFLAGS  = $(IM_NIMF_GTK3_DEPS_LIBS) -avoid-version -module
im_nimf_gtk3_la_LIBADD   = $(top_builddir)/libnimf/libnimf.la

DISTCLEANFILES = Makefile.in

install-data-hook:
	chmod -x $(DESTDIR)$(gtk3_im_moduledir)/im-nimf-gtk3.so
	rm -f $(DESTDIR)$(gtk3_im_moduledir)/im-nimf-gtk3.la

uninstall-hook:
	rm -f $(DESTDIR)$(gtk3_im_moduledir)/im-nimf-gtk3.so
	$(GTK_QUERY_IMMODULES3) --update-cache
