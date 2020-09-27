There are shell scripts in the build folder for unpacking and installing various camera vendor SDK packages.

To run these scripts, you need to be in an environment that can run a bash shell script. On Windows I use cygwin. Mac should work without any extra prerequisites.

### Altair SDK
```
./build/unpack_altaircam_sdk altaircamsdk.zip
```

### QHY SDK
```
./build/unpack_qhy_sdk.sh SDK_FILE...
```
Each SDK_FILE should be one of the SDK package files acquired from QHY (.zip for Windows, .tgz for Linux or Mac)

### Toupcam SDK
```
./build/unpack_toupcam_sdk.sh toupcamsdk.zip
```

### ZWO SDK
```
./build/unpack_zwo_libs ASI_linux_mac_SDK_<version>.tar ASI_Windows_SDK_<version>.zip
```

