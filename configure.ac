#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.64])
AC_INIT([tallow], [21], [auke-jan.h.kok@intel.com])
AM_INIT_AUTOMAKE([foreign -Wall -Werror -Wno-portability silent-rules subdir-objects color-tests
	no-dist-gzip dist-xz])
AC_CONFIG_FILES([Makefile])

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL

AC_CHECK_PROG([PANDOC],[pandoc],yes)
if test x"${PANDOC}" != x"yes" ; then
    AC_MSG_ERROR([Pandoc is required to create manual pages.])
fi

PKG_CHECK_MODULES(PCRE, libpcre)
PKG_CHECK_MODULES(JSON_C, json-c)
PKG_CHECK_MODULES(LIBSYSTEMD, libsystemd,, [PKG_CHECK_MODULES(LIBSYSTEMD, libsystemd-journal)])
AC_SUBST(LIBSYSTEMD_CFLAGS)
AC_SUBST(LIBSYSTEMD_LIBS)
AC_SUBST(LIBSYSTEMD_JOURNAL_CFLAGS)
AC_SUBST(LIBSYSTEMD_JOURNAL_LIBS)

AC_ARG_WITH([systemdsystemunitdir], AC_HELP_STRING([--with-systemdsystemunitdir=DIR],
	[path to systemd system service directory]), [path_systemdsystemunit=${withval}],
	[path_systemdsystemunit="`$PKG_CONFIG --variable=systemdsystemunitdir systemd`"])
if (test -n "${path_systemdsystemunit}"); then
SYSTEMD_SYSTEMUNITDIR="${path_systemdsystemunit}"
AC_SUBST(SYSTEMD_SYSTEMUNITDIR)
fi

AC_CHECK_HEADERS([stdlib.h stdio.h string.h stdarg.h limits.h sys/time.h])

AC_OUTPUT([
data/tallow.service
])
