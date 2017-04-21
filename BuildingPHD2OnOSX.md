# Building PHD2 on OSX #

  * Install CMake, the cross-platform build system

> http://www.cmake.org/download/

NOTE: newer versions of CMake like 3.8.0 do not currently work for building PHD2. CMake version 3.5.2 is known to work, so please install that version for building PHD2.

  * Install Xcode 4 or Xcode 5

> Our official builds are done with Xcode 4, but Xcode 5 can be used for development.

  * Download and build wxWidgets-3.0.2

> http://wxwidgets.org/downloads/

cd to the wxWidgets-3.0.2 source directory and run the following commands to build wxWidgets 32-bit static libs and install them to a location $WXWIN

```
./configure --enable-universal_binary=i386,x86_64 --disable-shared --with-libpng=builtin --with-cocoa --prefix=$WXWIN \
             --with-macosx-sdk=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.9.sdk/ \
             --with-macosx-version-min=10.7 \
             CXXFLAGS="-stdlib=libc++ -std=c++11" \
             OBJCXXFLAGS="-stdlib=libc++ -std=c++11" \
             CPPFLAGS="-stdlib=libc++"  \
             LDFLAGS="-stdlib=libc++" CXX=clang++ CXXCPP="clang++ -E" CC=clang CPP="clang -E"
make
make install
```

  * Get the phd2 source code from GitHub

```git clone https://github.com/OpenPHDGuiding/phd2.git```

You can clone the phd2 repo into a directory of your choice. We'll refer to this location as $PHD2\_SRC.

  * Generate the XCode project file

```
cd $PHD2_SRC
mkdir -p tmp
cd tmp
cmake -G Xcode -DwxWidgets_PREFIX_DIRECTORY=$WXWIN ..
```

  * Build and run PHD2

Open the Xcode project and build with Xcode:

> $PHD2\_SRC/tmp/PHD2.xcodeproj

The build produces the PHD2 app in:

> $PHD2\_SRC/tmp/PHD2.app
