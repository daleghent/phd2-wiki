# Building PHD2 on OSX

#### Install CMake version 3.5.2

> http://www.cmake.org/download/

NOTE: newer versions of CMake like 3.8.0 do not currently work for building PHD2. CMake version 3.5.2 is known to work, so please install that version for building PHD2.

#### Install Xcode 4 or newer and the Xcode Command Line Tools

> Our published builds are done with Xcode 4, but any newer version can be used for development.

#### Install the MacOSX10.7 SDK to support deploying PHD2 on older Macs

> Download Xcode 4.6.3 from developer.apple.com, extract the MacOSX10.7.sdk folder and put it under /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs

#### Download and build wxWidgets-3.0.3

> http://wxwidgets.org/downloads/

cd to the wxWidgets-3.0.3 source directory and run the following commands to build wxWidgets 32-bit static libs and install them to a location $WXWIN

```
./configure --enable-universal_binary=i386,x86_64 --disable-shared --with-libpng=builtin --with-cocoa --prefix=$WXWIN \
             --with-macosx-sdk=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.7.sdk/ \
             --with-macosx-version-min=10.7 \
             CXXFLAGS="-stdlib=libc++ -std=c++11" \
             OBJCXXFLAGS="-stdlib=libc++ -std=c++11" \
             CPPFLAGS="-stdlib=libc++"  \
             LDFLAGS="-stdlib=libc++" CXX=clang++ CXXCPP="clang++ -E" CC=clang CPP="clang -E"
make
make install
```

#### Install GNU gettext

> an easy way to install gettext is to install [Mac Ports](https://www.macports.org/install.php), then ```port install gettext```

#### Install the INDI client library.

We have a pre-built library that can be used, or you can build from source.

  * option 1: install pre-built library

```
curl -O https://openphdguiding.org/indiclient-e1edfb66-OSX-i386.tar.gz
sudo tar xfz indiclient-e1edfb66-OSX-i386.tar.gz -C /opt/local
```

  * option 2: build INDI client from source

      * install macports
      * configure macports to build i386 binaries by adding the following line to `/opt/local/etc/macports/macports.conf`

```
build_arch i386
```

  *
    * install the INDI client build prerequisites:

```
sudo port install cfitsio
```

  *
    * build the INDI client library:

```
git clone https://github.com/indilib/indi.git
mkdir indi_client_build
cd indi_client_build
cmake -DCMAKE_INSTALL_PREFIX=/opt/local \
  -DCMAKE_OSX_DEPLOYMENT_TARGET="10.9" \
  -DCMAKE_OSX_ARCHITECTURES=i386 \
  -DINDI_BUILD_SERVER=OFF -DINDI_BUILD_DRIVERS=OFF \
  -DINDI_BUILD_CLIENT=ON -DINDI_BUILD_QT5_CLIENT=OFF \
  . ../indi/libindi
make
sudo make install
```

#### Get the phd2 source code from GitHub

```git clone https://github.com/OpenPHDGuiding/phd2.git```

#### Generate the Makefiles

```
cd phd2
mkdir -p tmp
cd tmp
cmake -G "Unix Makefiles" -DwxWidgets_PREFIX_DIRECTORY=$WXWIN ..
```

#### Build PHD2

> make

This will build `PHD2.app`
