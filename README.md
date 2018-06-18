# android-tools

Git repository to make it easier to package certain command line
utilities provided by [android-tools][android-tools].

# Status

This is currently work in progress and there is still a lot of work to
do. Nonetheless, this build system is already used for the android-tools
[Alpine Linux package][alpine-linux].

The following tools can currently be build on Alpine Linux Edge but have
not been tested on different distributions and probably do not build on
them without additional patches:

	* [x] adb
	* [x] fastboot
	* [ ] e2fsdroid
	* [ ] mkbootimg
	* [x] mke2fs.android
	* [ ] ext2simg

# Motivation

[Many][void-linux] [Linux][arch-linux] [distribution][alpine-linux] have
a package called android-tools which ships essential android command
line tools like adb or fastboot. Sadly the upstream build system for
those tools is rather complex and doesn't allow building the command
line tools only.

Linux Distribution therefore mostly ship their own build systems for
building the command line utilities. This Repository aims to make
packaging of android command utilities easier by providing a simple
CMake based build system and a ready-to-use tarball which doesn't
require cloning all of the required git repositories manually. Besides
this makes it easy to collect all patches required to build standalone
android command line utilities in a central place.

# Dependencies

The following libraries are required by android-tools:

1. [libusb][libusb]
2. [PCRE][PCRE]
3. [Google Test][gtest]

*Currently the build system doesn't check whether these are installed.*

# Installation

Source tarballs containing an already patched version of all vendored
dependencies are available on the [GitHub Release Page][release-page].

These tarballs should be used for packaging and general installation.
After the tarball was downloaded and extracted android-tools can be
build and installed as follows:

	$ mkdir build && cd build
	$ cmake ..
	$ make
	$ make install

# Generating tarballs

New source tarballs can be created from the Git repository using:

	$ mkdir build && cd build
	$ cmake ..
	$ make package_source

Before a new release is uploaded a new `git-tag(1)` should be created
for the release. Afterwards the tarball can be uploaded to the [GitHub
Release Page][release-page].

# See also

The Arch Linux [android-tools package] by Anatol Pomozov which
inspired this project. Most definitions in the `CMakeLists.txt`
have been copied from Anatol's ruby script.

[android-tools]: https://sites.google.com/a/android.com/tools/
[void-linux]: https://github.com/voidlinux/void-packages/tree/master/srcpkgs/android-tools
[arch-linux]: https://www.archlinux.org/packages/community/x86_64/android-tools/
[alpine-linux]: https://pkgs.alpinelinux.org/package/edge/testing/x86_64/android-tools
[release-page]: https://github.com/nmeum/android-tools/releases
[libusb]: http://libusb.info/
[PCRE]: http://pcre.sourceforge.net/
[gtest]: https://github.com/google/googletest
