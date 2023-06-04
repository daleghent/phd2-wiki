# Building PHD2 on macOS - 64-bit

Instructions for building a 64-bit version of PHD2 that will run on macOS 10.14 Mojave or newer

#### Install MacPorts

The build will be using a few tools from [MacPorts](https://www.macports.org/). [HomeBrew](https://brew.sh/) should work just as well but I have not tried it.

#### Install CMake

```port install cmake```

#### Install Xcode and the Xcode Command Line Tools

We really just need the command-line tools, we won't be using XCode itself.

#### Download and build wxWidgets-3.1.7

> https://wxwidgets.org/downloads/

Run the following commands to build wxWidgets static libs and install them to a location $WXWIN

```
mkdir wxWidgets-3.1.7-build
cd wxWidgets-3.1.7-build
/path/to/wxWidgets-3.1.7/configure --disable-shared --with-libpng=builtin --with-cocoa --prefix=$WXWIN \
 --with-macosx-sdk=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX11.1.sdk \
 --with-macosx-version-min=10.14 \
 --with-regex=builtin \
 --with-libiconv=builtin
make
make install
```

#### Get the phd2 source code from GitHub

```git clone https://github.com/OpenPHDGuiding/phd2.git```

#### Generate the Makefiles

The `run_cmake-osx` script will run `cmake`, but expects to have `wx-config` on the PATH.  If you installed the wxWidgets in $WXWIN, then add `$WXWIN/bin` to your `PATH`:

```
PATH=$WXWIN/bin:$PATH
```

Run cmake

```
cd phd2
./run_cmake-osx 64
```

#### Build PHD2

```
cd tmp
make
```

This will build `PHD2.app`
