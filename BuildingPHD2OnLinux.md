# Instructions for building PHD2 on Linux #

## Step 1: Build Dependencies ##
### Fedora-like systems ###

  * Install dependencies (commands for a Fedora-like system; your system may vary)
```
sudo dnf install git cmake pkgconfig wxGTK3-devel libindi-devel libindi-static \
   libnova-devel zlib-devel libusb-devel libcurl-devel opencv-devel eigen3-devel gtest
```

### Debian-based systems (Ubuntu, Raspbian, ...) ###

  * Install dependencies -- debian bookworm example, your distro may differ
```
sudo apt-get install build-essential git cmake pkg-config libwxgtk3.2-dev \
   wx-common wx3.2-i18n libindi-dev libnova-dev gettext zlib1g-dev libx11-dev \
   libcurl4-gnutls-dev libopencv-dev libeigen3-dev libgtest-dev
```

### INDI version requirement ###

PHD2 requires a version of INDI newer than version 2.0. 
To use your provided INDI version, for example from the [INDI ppa](https://launchpad.net/~mutlaqja/+archive/ubuntu/ppa) use : `-DUSE_SYSTEM_LIBINDI=1`

If you not specify this option, INDI is automatically downloaded and compiled.

## Step 2: Build PHD2 ##

  * Get the PHD2 sources

```
  git clone https://github.com/OpenPHDGuiding/phd2.git
  cd phd2
```

  * Generate the Makefiles

```
  mkdir -p tmp
  cd tmp
  cmake ..
```

By default PHD2 incorporates binary drivers from some camera manufacturers (QHY and ZWO). If you would prefer to exclude binary drivers and produce a PHD2 binary based only on open source code, use this cmake command:

```
  mkdir -p tmp
  cd tmp
  cmake -DOPENSOURCE_ONLY=1 ..
```

  * Build PHD2

```
  make
```

Once PHD2 is built, you can either run PHD2 from the local build directory

```
  ./phd2
```

or install PHD2 onto the system

```
  sudo make install
```

### Note for 32bit i386 system ###

There is a bug in the Eigen library that prevent it to work correctly on i386 system when compiled with GCC 7 or newer. [See bug report](https://github.com/OpenPHDGuiding/phd2/issues/608).

If your distribution include GCC 7 by default the solution is to compile PHD2 with GCC 6.

  * Install GCC 6
```
  sudo apt-get install gcc-6 g++-6
```
  * Run cmake by specifying the compiler to use
```
  cmake -DCMAKE_C_COMPILER=gcc-6 -DCMAKE_CXX_COMPILER=g++-6 ..
```

---


# Build Debian packages #

The following notes are only to build a debian package that can be installed on other computer. This is not necessary if you only need PHD2 on a single computer.

## Prepare the system with the required packages ##

If you plan to build the packages locally on your computer you need to install all the prerequisite described above.

You also need to install the specific Debian build tools, this is done by installing the following meta package:
```
sudo apt-get install packaging-dev
```

If you want to sign the package (required for uploading) you need to setup a gpg and a ssh key. See http://packaging.ubuntu.com/html/getting-set-up.html

## Prepare the source tar ##

We need to start with a copy of the source code located in a directory named with the full version name, here 2.6.11 is used as an example, you must replace it by the current version in all the following commands. This directory must not include any git information. For that we use Github subversion compatibility command: "svn export":
```
svn export https://github.com/OpenPHDGuiding/phd2/trunk phd2_2.6.11
```
Then we remove some files not used by Linux:
```
cd phd2_2.6.11
rm -rf extra_frameworks WinLibs *.a
```
Update the files in the phd2\_2.6.11/debian directory. Be careful that every character in this files is important for the build process. Refer to the Debian documentation if your are not familiar with this files.
  * The file "changelog" must be updated to include the new version you package and the target system you want to build.
  * The file "control"  must be checked to add every new build dependency.
  * The file "copyright" must be updated to match the content of the PHD2 About dialog.

Create the versioned source tar:
```
cd ..
tar cvzf phd2_2.6.11.orig.tar.gz phd2_2.6.11
```

## Build the package locally ##

Even if you plan to upload the source package it is a good idea to test if it builds correctly on your system.
```
cd phd2_2.6.11
debuild -us -uc
```
You can now test the resulting .deb on your system.

## Build the package on a Launchpad PPA ##

We need to build a source package that is later uploaded to the PPA and compiled there. If we want to target many Ubuntu version we need to repeat the process for every version after updating the file debian/changelog.

Only the first package build for a new version must include the source tar `*`.orig.tar.gz. Use the following command to build it:
```
cd phd2_2.6.11
debuild -S -sa
```

To build for another version of Ubuntu, change the Ubuntu version in debian/changelog.
Make the source package without `*`.orig.tar.gz :
```
debuild -S -sd
```

Upload the source packages to the PPA, first the one with the source tar:
```
dput ppa:username/ppaname phd2_2.6.11-0ppa1~ubuntu20.04_source.changes
dput ppa:username/ppaname phd2_2.6.11-0ppa1~ubuntu22.04_source.changes
```

Connect to the PPA and check the build result for every version and architecture.