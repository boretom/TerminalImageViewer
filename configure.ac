dnl require autoconf 2.60 (AS_ECHO/AS_ECHO_N)
AC_PREREQ([2.60])

AC_CONFIG_MACRO_DIR([m4])

AC_INIT(tiv, 1.0)
AM_INIT_AUTOMAKE([subdir-objects -Wall -Werror foreign ])

# Switch to a C++ compiler, and check if it works
AC_LANG(C++)
# Especally for macOS since clang won't support <experimental/filesystem>
# up to including macOS 10.14. You want to install gcc or llvm with homebrew
AC_PROG_CXX([g++-9 g++-8 g++ clang++ llvm-g++])

AM_CONFIG_HEADER(config.h)

# Indicate this is a release build and that
# dependancies for changes between Makefile.am and Makefile.in
# should not be checked. This makes compiling faster. If you are working
# on the library, run: ./configure --enable-maintainer-mode to enable the dependancies
dnl AM_MAINTAINER_MODE

AC_CANONICAL_HOST

# Require C++11 compiler
AX_CXX_COMPILE_STDCXX([11], [noext], [mandatory], [nodefault])

AC_CHECK_HEADER(experimental/filesystem, ,[AC_MSG_ERROR([Could not find experimental/filesystem...libstdc++fs developement package required])])
AC_MSG_CHECKING([for experimental/filesystem::is_directory() support])
AC_COMPILE_IFELSE([
		AC_LANG_PROGRAM([
				#include <experimental/filesystem>
			],
			[
				std::experimental::filesystem::is_directory("some-dir");
			])], AC_MSG_RESULT([yes]),
				AC_MSG_RESULT([[no]])
				AC_MSG_ERROR([[experimental/filesystem::is_directory is needed, on macOS install GNU gcc using `brew`]])
		)

#			 [ax_cv_cxx_have_filesystem_dir=yes], [ax_cv_cxx_have_filesystem_dir=no]
#		)
#AS_IF([test "x$ax_cv_cxx_have_filesystem_dir" = "xyes"], [
#  AC_MSG_NOTICE([Do the stuff needed for enabling the feature])
#])
#AS_IF([test "x$ax_cv_cxx_have_filesystem_dir" = "xno"], [
#  AC_MSG_NOTICE([Don't the stuff needed for enabling the feature])
#])
# g++-9 -std=c++11 -lstdc++fs -o - conftest.cpp

AC_CONFIG_FILES([
 Makefile
])
dnl Process Makefile.in to create Makefile
AC_OUTPUT
