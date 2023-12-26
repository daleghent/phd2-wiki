# Building PHD2 on macOS - 64-bit

Instructions for building a 64-bit version of PHD2 that will run on macOS 14.0 Sonoma or newer

#### Install Homebrew

The build will be using a few tools and libraries from [HomeBrew](https://brew.sh/). Macports should work just as well it you prefer that.

#### Install CMake

```brew install cmake```

#### Install Xcode and the Xcode Command Line Tools

We really just need the command-line tools, we won't be using XCode itself.

#### Download and build wxWidgets-3.1.7

> https://wxwidgets.org/downloads/

Run the following commands to build wxWidgets static libs and install them to a location $WXWIN

```
mkdir wxWidgets-3.1.7-build
cd wxWidgets-3.1.7-build
/path/to/wxWidgets-3.1.7/configure --disable-shared --with-cocoa --prefix=$WXWIN \
 --with-macosx-sdk=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX14.0.sdk \
 --with-macosx-version-min=14.0 \
 --with-libpng=builtin \
 --with-regex=builtin \
 --with-libiconv=builtin \
 --with-libtiff=builtin \
 --without-libcurl
make
make install
```

#### Install build dependencies

```
brew install libnova cfitsio
```

#### Get the phd2 source code from GitHub

```
git clone https://github.com/OpenPHDGuiding/phd2.git
```

#### Generate the Makefiles

Run cmake

```
cd phd2
./run_cmake-osx
```

#### Build PHD2

```
cd tmp
make
```

This will build `PHD2.app`
