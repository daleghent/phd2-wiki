### PHD2 Camera Support ###

Please help us keep this page up to date!  You can edit this page if you have a github account.  If you do not have a github account and do not want to get one, then please post on the [PHD2 Forum](https://groups.google.com/forum/?fromgroups=#!forum/open-phd-guiding) and let us know what you would like to see updated.

**NOTE**: If you do not see your camera in the list below, or if it is marked as not supported, you may still be able to use it with PHD2.  If the camera has an available ASCOM driver (Windows) or an INDI driver (Linux), then you _can_ use the camera with PHD2.

|Camera|Windows|Mac 32-bit|Mac 64-bit|Linux|Notes|
|------|:-----:|:--------:|:--------:|:---:|-----|
| Altair Cameras | **Yes** | **Yes** | **Yes** | **Yes** | Windows: native mode or use Altair ASCOM driver, or INDI<br>Mac and Linux: use INDI |
| ASCOM Cameras| **Yes** | No | No | No | Linux/Mac available through WINDI |
| Astromania Cameras| | | | | See ToupTek below |
| Atik 16 series | **Yes** | No | No | No | color and mono. If your Atik 16 camera is not recognized by PHD2, try updating to the latest drivers from Atik and try connecting as "Atik Gen3" in PHD2. |
| Atik Gen 3  | **Yes** | No | No | No | color and mono |
| CCD Labs Q-Guider | **Yes** | No | No | No |  |
| Fishcamp Starfish | **Yes** | **Yes** | No | No |  |
| i-Nova PLC-M | **Yes** | No | No | No | |
| INDI Cameras| **Yes** | **Yes** | **Yes** | **Yes** | [INDI camera list](http://www.indilib.org/devices/ccds.html) |
| iOptron iGuider | **Yes** | No | No | No |  [iOptron iGuider info](#ioptron) |
| KWIQGuider | No | **Yes** | **Yes** | No |  [*] Mac 64 unconfirmed |
| Long exposure webcams | **Yes** | No | No | No | USB, Parallel, or serial interface |
| MagZero MZ-5 | **Yes** | No | No | No |  |
| MallinCam SkyRaider | **Yes** | **Yes** | **Yes** | **Yes** | Windows: select ToupTek Camera, or connect as a WDM webcam or as an ASCOM camera (download the ASCOM driver from [Mallincam software downloads](http://www.mallincam.net/software-downloads.html))<br>Mac 32-bit: supported natively<br>Mac 64-bit and Linux: Connect as ToupTek camera |
| Meade DSI I, II, or III | **Yes** | **Yes** | No | No |  |
| Moravian Cameras | **Yes** | **Yes** | **Yes** | **Yes** | Windows: native, ASCOM, or INDI<br>Mac and Linux: use the Moravian INDI driver<br>[Moravian info](#moravian) |
| Omegon Pro Cameras | **Yes** | No | **Yes** | **Yes** | [Touptek info](#touptek)|
| OpenCV webcam | **Yes** | No | No | No |  |
| Orion StarShoot Autoguider | **Yes** | **Yes** | **Yes** | **Yes** (see [here](https://github.com/OpenPHDGuiding/phd2/issues/496)) | Note: [How to connect to an SSAG with corrupted firmware](Orion-Starshoot-Autoguider-VID---PID-Override) |
| Orion Starshoot DSCI | **Yes** | No | No | No |  |
| Orion StarShoot Planetary Imager and Autoguider | **Yes** | No | No | No |  |
| QHY5 | No | No | No | **Yes** | |
| QHY Cameras | **Yes** | **Yes** | **Yes** | **Yes** | (cameras more recent than the QHY5)<br>[QHY Support Info](http://www.qhyccd.com/file/repository/PDF/HowToAvoidCameraHangissue(QHY5L-II)_EN.pdf) |
| SAC4-2 | **Yes** | No | No | No |  |
| SBIG cameras | **Yes** | **Yes** | **Yes** | No | [SBIG info](#sbig) |
| Simulator | **Yes** | **Yes** | **Yes** | **Yes** | PHD2's built-in camera simulator, great for development and learning PHD2 |
| Starlight Xpress cameras | **Yes** | **Yes** | **Yes** | **Yes** |[SX info](#sx)|
| Svbony cameras | **Yes** | No(*) | **Yes** | **Yes** | 32-bit Mac no longer supported in v2.6.11dev3; may work in earlier versions |
| The Imaging Source cameras | **Yes** | **Yes** | **Yes** | **Yes** | On Windows select "Windows WDM-style webcam" or use the [TIS ASCOM camera driver](http://www.deepsky-online.com/). For OSX and Linux, use the [TIS INDI Driver](http://www.indilib.org/devices/ccds/imaging-source-ccd.html). OSX also has a builtin driver (DCAM Firewire). |
| ToupTek Cameras | **Yes** | No | **Yes** | **Yes** | [Touptek info](#touptek)|
| Windows WDM-style webcams | **Yes** | No | No | No | |
| ZWO ASI cameras| **Yes** | **Yes** | **Yes** | **Yes** |[ZWO info](#sx)|

<a name=sbig></a>
### SBIG Cameras ###

SBIG cameras only allow a single application at a time to access the camera. If the camera is one of the self-guiding models with a built-in guide camera, then the imaging app controlling the imaging chip will need to provide access to the guide camera. The only app we know of with this capability is Sequence Generator Pro which exposes the internal guide camera to PHD2 as an ASCOM camera.

<a name=sx></a>
### Starlight Xpress Cameras ###
On Windows you can connect to your SX camera in two ways: with the ASCOM driver or the PHD2 built-in driver, "Starlight Xpress SXV".  If you are using the ASCOM driver and want to use a Bad-pixel map in PHD2, then make sure that you disable the ASCOM driver options Square Lodestar Pixels and Gaussian Blur as these options will interfere with PHD2 being able to identify hot pixels.

<a name=zwo></a>
### ZWO Cameras ###
ZWO ASI cameras are supported natively on Windows, Mac, and Linux.
The cameras can also be accessed with ASCOM or INDI camera drivers.
On Linux, the USB 2.0 cameras may require that you flash the firmware version labeled "compatible" [Forum Thread](https://groups.google.com/d/msg/open-phd-guiding/u0qpmEDOxPI/tR2NeOpMAwAJ).

<a name=touptek></a>
### ToupTek Cameras ###

On Windows ToupTek camera support is built-in to PHD2, or you can use the ToupTek's ASCOM camera driver.  Linux native support should also work, but it has not been tested yet.  On Mac, you'll need the 64-bit version of PHD2 as  ToupTek no longer provides SDK support for 32-bit Macs.

<a name=iOptron></a>
### iOptron iGuider ###
The camera's gain and exposure time can be set by clicking the camera properties button on the toolbar.
See this [forum post](https://groups.google.com/d/msg/open-phd-guiding/WWY_tdKCpw8/dbZPCzyAHm0J) for a description of how the camera's exposure time relates to PHD2's exposure duration setting.

Here is the information from iOptron showing the camera's available gain and exposure values:

![](https://user-images.githubusercontent.com/6864470/72243056-df9bb680-35b8-11ea-9b28-70d2e2108cd2.png)

<a name=moravian></a>
### Moravian Cameras ###
- The Moravian SDK is Windows-only, so native Moravian camera support is only available on Windows. Use the Moravian INDI driver for Mac and Linux.
- Currently PHD2's native support covers the gXusb-type cameras -- everything but the large cooled C3 and C4 cameras.
- Cameras connected through the Moravian Camera Ethernet adapter are not supported, though we could add support for that if there is a demand.