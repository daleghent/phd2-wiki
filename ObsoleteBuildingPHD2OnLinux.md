# Instructions for building PHD2 on Linux #

## Build Dependencies ##
### Fedora-like systems ###

  * install dependencies (commands for a Fedora-like system; your system may vary)
```
sudo yum install subversion gtk2-devel cfitsio-devel opencv-devel libusb1-devel cmake libudev-devel libv4l-devel libindi-devel libnova-devel
```

### Ubuntu ###

  * install dependencies (tested on 14.04 and 14.10)
```
sudo apt-get install build-essential libgtk2.0-dev libcfitsio3-dev libopencv-dev libusb-1.0-0-dev subversion cmake libudev-dev libv4l-dev libindi-dev libnova-dev
```

### wxWidgets-3.0.2 ###

  * download and extract wxWidgets 3.0.2 or later from http://wxwidgets.org
```
# cd into the extracted wx 
cd wxWidgets-3.0.2/

# change files to have unix newlines, this is needed for at least all python and shell scripts
find . -type f -print -exec perl -p -i -e "s/\r\n/\n/" {} \;

cd build/
../configure --with-libpng=builtin --with-regex=builtin --with-libjpeg=builtin --with-libtiff=builtin --with-expat=builtin --disable-shared
make
sudo make install
```

If you prefer not to install this wxWidgets build on your system, and just use it for building PHD2, add the following to option to configure:

`--prefix=WXDIR`

replacing `WXDIR` with a location of your choice. Then, add `WXDIR/bin` to your PATH before building PHD2 as described below.

## phd2 ##

  * get the phd2 sources
```
svn checkout http://open-phd-guiding.googlecode.com/svn/trunk/ open-phd-guiding
```

  * build phd2
<a href='Hidden comment:     * either via make (in-tree)
```
cd open-phd-guiding
make
```
'></a>
    * via cmake (out-of-tree)
```
mkdir open-phd-guiding-build; cd open-phd-guiding-build
cmake ../open-phd-guiding/
make
```

  * run phd2
```
./phd2
```



---


# Build Debian packages #

## Prepare the system with the required packages ##

If you plan to build the packages locally on your computer you need to install all the prerequisite described above.

You also need to install the specific Debian build tools, this is done by installing the following meta package:
```
apt-get install packaging-dev
```

If you want to sign the package (required for uploading) you need to setup a gpg and a ssh key. See http://packaging.ubuntu.com/html/getting-set-up.html

## Prepare the source tar ##

We need to start with a copy of the source code located in a directory named with the full version name, here 2.4.1 is used as an example, you must replace it by the current version in all the following commands. This directory must not include any subversion information. For that we use the "svn export" command:
```
svn export http://open-phd-guiding.googlecode.com/svn/trunk phd2_2.4.1
```
Then we remove some files not used by Linux:
```
cd phd2_2.4.1
rm -rf extra_frameworks WinLibs *.a
```
Ensure the help file is updated for all the languages:
```
cd build
./build_help.sh
```
Update the files in the phd2\_2.4.1/debian directory. Be careful that every character in this files is important for the build process. Refer to the Debian documentation if your are not familiar with this files.
  * The file "changelog" must be updated to include the new version you package and the target system you want to build.
  * The file "control"  must be checked to add every new build dependency.
  * The file "copyright" must be updated to match the content of the PHD2 About dialog.

Create the versioned source tar:
```
tar cvzf phd2_2.4.1.orig.tar.gz phd2_2.4.1
```

## Build the package locally ##

Even if you plan to upload the source package it is a good idea to test if it build correctly on your system.
```
cd phd2_2.4.1
debuild -us -uc
```
You can now test the resulting .deb on your system.

## Build the package on a Launchpad PPA ##

We need to build a source package that is later uploaded to the PPA and compiled there. If we want to target many Ubuntu version we need to repeat the process for every version after updating the file debian/changelog.

Only the first package build for a new version must include the source tar `*`.orig.tar.gz. Use the following command to build it:
```
cd phd2_2.4.1
debuild -S -sa
```

Change the Ubuntu version in debian/changelog:
```
sed -i '/2.4.1/s/trusty/utopic/g' debian/changelog
```
Make the source package without `*`.orig.tar.gz :
```
debuild -S -sd
```

Upload the source packages to the PPA, first the one with the source tar:
```
dput ppa:username/ppaname phd2_2.4.1-0ppa1~trusty1_source.changes
dput ppa:username/ppaname phd2_2.4.1-0ppa1~utopic1_source.changes
```

Connect to the PPA and check the build result for every version and architecture.