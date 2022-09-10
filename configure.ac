dnl Process this file with autoconf to produce a configure script.

AC_INIT([nimf],[1.3.0])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])

AM_INIT_AUTOMAKE([subdir-objects -Wall -Werror])
AM_MAINTAINER_MODE([disable])
AM_SILENT_RULES([yes])

AM_PROG_AR

LT_INIT([disable-static])

dnl ***************************************************************************
dnl libnimf
dnl ***************************************************************************
# Before making a release, the LT_VERSION string should be modified.
# The string is of the form C:R:A.
# - If interfaces have been changed or added, but binary compatibility has
#   been preserved, change to C+1:0:A+1
# - If binary compatibility has been broken (eg removed or changed interfaces)
#   change to C+1:0:0
# - If the interface is the same as the previous version, change to C:R+1:A

LIBNIMF_LT_VERSION=1:0:0
AC_SUBST(LIBNIMF_LT_VERSION)

LIBNIMF_REQUIRES="glib-2.0 gio-2.0 gio-unix-2.0 gmodule-2.0"
AC_SUBST(LIBNIMF_REQUIRES)
PKG_CHECK_MODULES(LIBNIMF_DEPS, [$LIBNIMF_REQUIRES])

dnl ***************************************************************************
dnl nimf-system-keyboard
dnl ***************************************************************************

PKG_CHECK_MODULES(NIMF_SYSTEM_KEYBOARD_DEPS,
                                       [xkbcommon >= 0.5.0  $LIBNIMF_REQUIRES])

dnl ***************************************************************************
dnl nimf-rime
dnl ***************************************************************************

AC_ARG_ENABLE([nimf-rime],
              AS_HELP_STRING([--disable-nimf-rime], [Disable nimf-rime]))

AS_IF([test "x$enable_nimf_rime" != "xno"],
      [PKG_CHECK_MODULES(NIMF_RIME_DEPS, [rime >= 1.2.9 $LIBNIMF_REQUIRES])])

AM_CONDITIONAL([ENABLE_NIMF_RIME], [test "x$enable_nimf_rime" != "xno"])

dnl ***************************************************************************
dnl  Check for im-nimf-gtk
dnl ***************************************************************************

PKG_CHECK_MODULES(IM_NIMF_GTK3_DEPS, [gtk+-3.0 gdk-x11-3.0])

case `uname -m` in
  x86_64|aarch64)
    BITS=64
    ;;
  *)
    BITS=32
    ;;
esac

GTK3_LIBDIR=`pkg-config --variable=libdir gtk+-3.0`
GTK3_BINARY_VERSION=`pkg-config --variable=gtk_binary_version gtk+-3.0`
AC_SUBST(GTK3_LIBDIR)
AC_SUBST(GTK3_BINARY_VERSION)
AC_PATH_PROGS([GTK_QUERY_IMMODULES3],
              [gtk-query-immodules-3.0 gtk-query-immodules-3.0-$BITS], [no],
              [/usr/bin:$GTK3_LIBDIR/libgtk-3-0])
if test "x$GTK_QUERY_IMMODULES3" = "xno"; then
  AC_MSG_ERROR([gtk-query-immodules-3.0 or gtk-query-immodules-3.0-$BITS not found])
fi

dnl ***************************************************************************
dnl  icon cache
dnl ***************************************************************************

AC_PATH_PROGS([GTK_UPDATE_ICON_CACHE],
              [gtk-update-icon-cache-3.0 gtk-update-icon-cache], [no],
              [/usr/bin:$GTK3_LIBDIR/libgtk-3-0:$GTK2_LIBDIR/libgtk2.0-0])
if test "x$GTK_UPDATE_ICON_CACHE" = "xno"; then
  AC_MSG_ERROR([gtk-update-icon-cache-3.0 or gtk-update-icon-cache not found])
fi

dnl ***************************************************************************
dnl nimf-wayland
dnl ***************************************************************************

#PKG_CHECK_MODULES(NIMF_WAYLAND_DEPS, [$LIBNIMF_REQUIRES]
#                                     wayland-client wayland-server
#                                     wayland-protocols xkbcommon)

dnl ***************************************************************************
dnl nimf-xim
dnl ***************************************************************************

PKG_CHECK_MODULES(NIMF_XIM_DEPS, [$LIBNIMF_REQUIRES] x11)

dnl ***************************************************************************
dnl nimf-nim
dnl ***************************************************************************

PKG_CHECK_MODULES(NIMF_NIM_DEPS, [$LIBNIMF_REQUIRES] glib-2.0 gio-2.0)

dnl ***************************************************************************
dnl nimf server
dnl ***************************************************************************

PKG_CHECK_MODULES(NIMF_DEPS, [glib-2.0 gio-2.0 gobject-2.0 gmodule-2.0])

dnl ***************************************************************************
dnl nimf-preedit-window  nimf-candidate
dnl ***************************************************************************

PKG_CHECK_MODULES(NIMF_PREEDIT_WINDOW_DEPS, [glib-2.0 gtk+-3.0])
PKG_CHECK_MODULES(NIMF_CANDIDATE_DEPS,      [glib-2.0 gtk+-3.0])

dnl ***************************************************************************
dnl nimf-settings
dnl ***************************************************************************

PKG_CHECK_MODULES(NIMF_SETTINGS_DEPS,
                  [gtk+-3.0 glib-2.0 >= 2.54 gio-2.0 gmodule-2.0 libxklavier
                   gdk-3.0 gdk-x11-3.0])

dnl ***************************************************************************

GLIB_GSETTINGS

AC_CONFIG_FILES([
  Makefile
  bin/Makefile
  bin/nimf/Makefile
  bin/nimf-settings/Makefile
  libnimf/Makefile
  libnimf/nimf.pc
  modules/Makefile
  modules/clients/Makefile
  modules/clients/gtk/Makefile
  modules/engines/Makefile
  modules/engines/nimf-rime/Makefile
  modules/engines/nimf-system-keyboard/Makefile
  modules/services/Makefile
  modules/services/candidate/Makefile
  modules/services/nim/Makefile
  modules/services/preedit-window/Makefile
  modules/services/xim/Makefile
])
AC_OUTPUT
