# Initialization
AC_PREREQ([2.69])
AC_INIT([openpower-dbus-interfaces], [1.0], [https://github.com/openbmc/openpower-dbus-interfaces])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([subdir-objects -Wall -Werror foreign dist-xz])
AM_SILENT_RULES([yes])
AC_LANG([C++])

# Checks for programs.
AC_PROG_CXX
AM_PROG_AR
AC_PROG_INSTALL
AC_PROG_MAKE_SET
AC_PROG_SED
AC_CHECK_PROG([FIND], find, find)
AC_CHECK_PROG([BASENAME], basename, basename)
AC_CHECK_PROG([DIRNAME], dirname, dirname)

AC_ARG_ENABLE([libopenpower_dbus],
    AS_HELP_STRING([--disable-libopenpower_dbus], [Disable libopenpower_dbus]))

AM_CONDITIONAL([WANT_LIBOPENPOWER_DBUS], [test "x$enable_libopenpower_dbus" != "xno"])

AS_IF([test "x$enable_libopenpower_dbus" != "xno"], [
    AC_PATH_PROG([SDBUSPLUSPLUS], [sdbus++])
    AS_IF([test "x$SDBUSPLUSPLUS" == "x"],
        AC_MSG_ERROR([Cannot find sdbus++]))

    # Check for baseline language coverage in the compiler for the C++14 standard
    AX_CXX_COMPILE_STDCXX_14([noext])
    AX_APPEND_COMPILE_FLAGS([-Wall -Werror], [CFLAGS])
    AX_APPEND_COMPILE_FLAGS([-Wall -Werror], [CXXFLAGS])

    # Checks for library functions.
    LT_INIT([dlopen disable-static shared])
    LT_LIB_DLLOAD

    # Create configured output
    AC_CONFIG_FILES([Makefile.interfaces],
        [${srcdir}/generate_makefile.sh ${srcdir} > Makefile.interfaces])
    AC_CONFIG_FILES([openpower-dbus-interfaces.pc])
])
AC_CONFIG_FILES([Makefile.yaml],
    [${srcdir}/generate_yaml_makefile.sh ${srcdir} > Makefile.yaml])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
