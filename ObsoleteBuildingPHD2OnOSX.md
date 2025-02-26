The easiest way to build PHD2 is to use pre-built dependent libraries as we describe here. At the bottom of the page are instructions for building the libraries yourself.

# Building PHD2 on OSX using pre-built dependencies #

  * Install xcode 4

  * Unpack the dependencies bundle [PHD2-OSX-devel-0.3.tar.bz2](http://adgsoftware.com/phd2/PHD2-OSX-devel-0.3.tar.bz2) into a location of your choice:
`tar xfj PHD2-OSX-devel-0.3.tar.bz2`

  * get phd2 sources

Checkout the open-phd-guiding source tree into this directory so that open-phd-guiding is a sibling of wxWidgets and the other stuff here, like this:

```
<top>
  +--- HID Utilities Source
  +--- cfitsio
  +--- libdc1394-2.0.0-rc7
  +--- libusb-1.0.9
  +--- open-phd-guiding
  +--- opencv
  +--- opencv-2.4.6.1
  +--- wxWidgets
  +--- wxWidgets-3.0.2
```

This is important because the PHD2 xcode project file will expect to find the dependencies via relative paths.

If you already have a wxWidgets source tree somewhere else that you would prefer to use, you can adjust the symlink to point to that location.

  * Unzip the following two frameworks in extra\_frameworks/ into /Library/Frameworks

```
  cd <top>
  unzip open-phd-guiding/extra_frameworks/SBIGUDrv.framework.zip -d /Library/Frameworks
  unzip open-phd-guiding/extra_frameworks/fcCamFw.framework.zip -d /Library/Frameworks
```

You should now be able to open the xcode project and build and run PHD2.

# Building the dependencies #

Here are some notes on how I built or acquired the dependencies.

## HID Utilities Source ##
This is in the source tree under extra\_frameworks, but the xcode project file wants it as a sibling, and not under /Library/Frameworks

```
cd <top>/open-phd-guiding/extra_frameworks
unzip 'HID Utilities Source.zip' -d ../../
```

## cfitsio ##
I got this from Bret, I assume it was: download, configure, and build

## libdc1394 ##
download libdc1394-2.0.0-rc7 from SourceForge http://sourceforge.net/projects/libdc1394/. It's important to get this specific version.

```
  ./configure --prefix=/opt/local --enable-shared=no
  make
```

## libusb ##
I used Mac ports to install the libusb dependencies. It's probably easier to just download and build them, but I was playing around with Mac ports at the time.

  * install Mac ports
  * edit /opt/local/etc/macports/macports.conf and change build\_arch like this:
```
build_arch i386
```
then
```
  sudo port install libusb @1.0.9
  sudo port install libusb-compat @0.1.4
```

  * copy the libusb and libusb-compat headers and static libs from /opt/local/ to libusb-1.0.9/
```
  cd <top>
  mkdir libusb-1.0.9/
  tar cf - -C /opt/local ./include/libusb-1.0/libusb.h ./include/usb.h ./lib/libusb-1.0.a ./lib/libusb.a | \
    tar xf - -C libusb-1.0.9/
```

## opencv ##
I got that from Bret. I'm not even sure we are using that yet on Mac.

## wxWidgets ##

Download the wxWidgets-3.0.2 sources from http://sourceforge.net/projects/wxwindows/files/

Unpack the sources in the directory containing open-phd-guiding.

Configure and build:

```
  cd wxWidgets-3.0.2
  mkdir Cocoa_32
  cd Cocoa_32
  ../configure --with-libpng=builtin --with-cocoa --disable-shared --with-macosx-version-min=10.6 --enable-macosx_arch=i386 --with-macosx-sdk=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.7.sdk
  make
```