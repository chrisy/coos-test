dnl Process this file with autoconf to produce a configure script.

AC_PREREQ(2.67)
AC_COPYRIGHT([(c) 2014 Chris Luke])

AC_INIT([coos-test], [0.1])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([aclocal])
AC_CANONICAL_TARGET

AM_INIT_AUTOMAKE([subdir-objects])

# Build programs
AC_PROG_MAKE_SET
AC_PROG_LN_S
AC_PROG_AWK
: ${CFLAGS="-nostartfiles"}
AC_PROG_CC
AC_PROG_CPP
AC_PROG_CXX
AC_PROG_CC_C99
AM_PROG_CC_C_O
LT_INIT
AC_DISABLE_SHARED
AC_ENABLE_STATIC
AC_PROG_LIBTOOL
AC_SUBST([LIBTOOL_DEPS])

# Compiler flags
#AX_CFLAGS_GCC_OPTION([-std=c99])
AX_CFLAGS_GCC_OPTION([-pipe])
AX_CFLAGS_GCC_OPTION([-mcpu=cortex-m3 -mthumb])

# Compiler flags part deux
AX_CFLAGS_GCC_OPTION([-Wall])
AX_CFLAGS_GCC_OPTION([-W])
AX_CFLAGS_GCC_OPTION([-Wextra])

# These are warnings included in -Wextra, but we don't want all of -Wextra
AX_CFLAGS_GCC_OPTION([-Wno-unused-parameter])
#AX_CFLAGS_GCC_OPTION([-Wno-sign-compare])

# And finally, be picky
AX_CFLAGS_GCC_OPTION([-Werror])
#AX_CFLAGS_GCC_OPTION([-pedantic])  # CoOS doesn't like -pedantic

# Debug mode
AC_ARG_ENABLE([debug],
  [AS_HELP_STRING([--enable-debug], [configure with debugging features enabled]) ]
)
if test x"$enable_debug" = xyes; then
  CPPFLAGS="$CPPFLAGS -D_DEBUG"
  ggdb=
  if test x`uname` = xLinux; then
    ggdb=gdb
  fi
  CFLAGS="$CFLAGS -O0 -g$ggdb"
  if test x"$enable_gprof" = xyes; then
    CFLAGS="$CFLAGS -pg"
  fi
else
  CFLAGS="$CFLAGS -O2 -g"
fi

# Add our various discovered flags
CPPFLAGS="$CPPFLAGS $LIBCURL_CPPFLAGS"
CFLAGS="$CFLAGS $PTHREAD_CFLAGS"
LIBS="$LIBS $LIBCURL $PTHREAD_LIBS"

# Headers
AC_CHECK_HEADERS([ stdlib.h ])

# Definitions (typedef, struct etc)
AC_C_INLINE
case "$ac_cv_c_inline" in
    yes) cc_inline=inline;;
    no) cc_inline=;;
    *) cc_inline="$ac_cv_c_inline";;
esac
AC_SUBST([cc_inline])

# Setup our include search paths
bdir="${srcdir}"
if test x"${bdir}" = x'.' ; then
	bdir=$(pwd)
fi
CPPFLAGS="$CPPFLAGS -I${bdir}/include -I${bdir}/CoOS/kernel -I${bdir}/CoOS/portable"

# Display the summary
CC=`echo $CC | sed -e 's/  / /g'`
CPPFLAGS=`echo $CPPFLAGS | sed -e 's/  / /g'`
CFLAGS=`echo $CFLAGS | sed -e 's/  / /g'`
LD=`echo $LD | sed -e 's/  / /g'`
LDFLAGS=`echo $LDFLAGS | sed -e 's/  / /g'`
LIBS=`echo $LIBS | sed -e 's/  / /g'`

echo "CC:       $CC" >&2
echo "CPPFLAGS: $CPPFLAGS" >&2
echo "CFLAGS:   $CFLAGS" >&2
echo "LD:       $LD" >&2
echo "LDFLAGS:  $LDFLAGS" >&2
echo "LIBS:     $LIBS" >&2
echo "srcdir:   $srcdir" >&2

# Output
AC_CONFIG_FILES([Makefile
	include/Makefile
	include/cc_config.h
	CoOS/Makefile])
AC_CONFIG_HEADER([include/ac_config.h])
AC_OUTPUT

