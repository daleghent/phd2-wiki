# Installing dependencies
Building PHD2 on FreeBSD requires its dependencies to be installed in the system. Make sure that the libraries below are available.

## Libraries to install
### Available using pkg/ports
* cfitsio
* eigen
* googletest
* wx31-gtk3

### Requires manual building
* libindi (master should build on FreeBSD, https://github.com/indilib/indi)

### Available in the base system (no install required)
* libusb

# Building
Configure the project to use system libraries and build using make. Execute the commands below in the project directory.
```
cmake . -DUSE_SYSTEM_CFITSIO=ON -DUSE_SYSTEM_EIGEN3=ON -DUSE_SYSTEM_GTEST=ON -DUSE_SYSTEM_LIBINDI=ON -DUSE_SYSTEM_LIBUSB=ON
make
```
To speed up the build, `make -j $threadcount` can be used.