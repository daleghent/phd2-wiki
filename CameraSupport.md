### PHD2 Camera Support ###

Please help us keep this page up to date!  You can edit this page if you have a github account.  If you do not have a github account and do not want to get one, then please post on the [PHD2 Forum](https://groups.google.com/forum/?fromgroups=#!forum/open-phd-guiding) and let us know what you would like to see updated.

**NOTE**: If you do not see your camera in the list below, or if it is marked as not supported, you may still be able to use it with PHD2.  If the camera has an available ASCOM driver (Windows) or an INDI driver (Linux), then you _can_ use the camera with PHD2.

|Camera|Windows|OSX|Linux|Notes|
|------|:-----:|:-:|:---:|-----|
| Altair Cameras | **Yes** | No | No | Native mode available for Windows, or use Altair ASCOM driver |
| ASCOM Cameras| **Yes** | No | No | Linux/Mac available through WINDI |
| Astromania Cameras| | | | See ToupTek below |
| Atik 16 series | **Yes** | No | No | color and mono. If your Atik 16 camera is not recognized by PHD2, try updating to the latest drivers from Atik and try connecting as "Atik Gen3" in PHD2. |
| Atik Gen 3  | **Yes** | No | No | color and mono |
| CCD Labs Q-Guider | **Yes** | No | No |  |
| Fishcamp Starfish | **Yes** | **Yes** | No |  |
| i-Nova PLC-M | **Yes** | No | No | |
| INDI Cameras| **Yes** | **Yes** | **Yes** | [INDI camera list](http://www.indilib.org/devices/ccds.html) |
| KWIQGuider | No | **Yes** | No |  |
| Long exposure webcams | **Yes** | No | No | USB, Parallel, or serial interface |
| MagZero MZ-5 | **Yes** | No | No |  |
| Mallincam SkyRaider | **Yes** | No | No | Connects as a WDM webcam or as an ASCOM camera (download the ASCOM driver from [Mallincam software downloads](http://www.mallincam.net/software-downloads.html)) |
| Meade DSI I, II, or III | **Yes** | **Yes** | No |  |
| OpenCV webcam | **Yes** | No | No |  |
| Orion StarShoot Autoguider | **Yes** | **Yes** | **Yes** (see [here](https://github.com/OpenPHDGuiding/phd2/issues/496)) | Note: [How to connect to an SSAG with corrupted firmware](Orion-Starshoot-Autoguider-VID---PID-Override) |
| Orion Starshoot DSCI | **Yes** | No | No |  |
| Orion StarShoot Planetary Imager and Autoguider | **Yes** | No | No |  |
| QHY5 | No | No | **Yes** | |
| QHY Cameras | **Yes** | **Yes** | **Yes** | (cameras more recent than the QHY5)<br>[QHY Support Info](http://www.qhyccd.com/file/repository/PDF/HowToAvoidCameraHangissue(QHY5L-II)_EN.pdf) |
| SAC4-2 | **Yes** | No | No |  |
| SBIG cameras | **Yes** | **Yes** | No | [SBIG info](#sbig) |
| Simulator | **Yes** | **Yes** | **Yes** | PHD2's built-in camera simulator, great for development and learning PHD2 |
| Starlight Xpress cameras | **Yes** | **Yes** | **Yes** |[SX info](#sx)|
| The Imaging Source cameras | **Yes** | **Yes** | **Yes** | On Windows select "Windows WDM-style webcam" or use the [TIS ASCOM camera driver](http://www.deepsky-online.com/). For OSX and Linux, use the [TIS INDI Driver](http://www.indilib.org/devices/ccds/imaging-source-ccd.html). OSX also has a builtin driver (DCAM Firewire). |
| ToupTek Cameras | **Yes** | No | No | [Touptek info](#touptek)|
| Windows WDM-style webcams | **Yes** | No | No | |
| ZWO ASI cameras| **Yes** | **Yes** | **Yes** |[ZWO info](#sx)|

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

On Windows ToupTek camera support is built-in to PHD2, or you can use the ToupTek's ASCOM camera driver.  Linux native support should also work, but it has not been tested yet.  ToupTek stopped providing a 32-bit Mac version of their SDK, so if you are a Mac user please contact ToupTek and encourage them to resume their support for 32-bit Mac.