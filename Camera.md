### PHD2 Camera Support ###

Please help us keep this page up to date!  You can edit this page if you have a github account.  If you do not have a github account and do not want to get one, then please post on the [PHD2 Forum](https://groups.google.com/forum/?fromgroups=#!forum/open-phd-guiding) and let us know what you would like to see updated.

|Camera|Windows|OSX|Linux|Notes|
|------|:-----:|:-:|:---:|-----|
| Altair Cameras | Yes | No | No |  |
| ASCOM Cameras| Yes | No | No | |
| Atik 16 series | Yes | No | No | color and mono |
| Atik Gen 3  | Yes | No | No | color and mono |
| CCD Labs Q-Guider | Yes | No | No |  |
| Fishcamp Starfish | Yes | Yes | No |  |
| i-Nova PLC-M | Yes | No | No | No |
| INDI Cameras|No|No|Yes| |
| KWIQGuider | No | Yes | No |  |
| Long exposure webcams | Yes | No | No | USB, Parallel, or serial interface |
| MagZero MZ-5 | Yes | No | No |  |
| Meade DSI, II, or III | Yes | Yes | No |  |
| OpenCV webcam | Yes | No | No |  |
| Orion StarShoot Autoguider | Yes | Yes | No |  |
| Orion Starshoot DSCI | Yes | No | No |  |
| Orion StarShoot Planetary Imager and Autoguider | Yes |  |  |  |
| QHY5 | No | No | Yes | |
| QHY5-II | Yes | No | No | [QHY info](#qhy) |
| QHY5L-II | Yes | No | No | color or mono<br>[QHY info](#qhy) |
| SAC4-2 | Yes | No | No |  |
| SBIG cameras | Yes | Yes | No | [SBIG info](#sbig) |
| Simulator | Yes | Yes | Yes | PHD2's built-in camera simulator, great for development and learning PHD2 |
| Starlight Xpress cameras |Yes|Yes|Yes||
| The Imaging Source (DCAM Firewire) | No | Yes | No |  |
| Windows WDM-style webcams | Yes | No | No |  |
| ZWO ASI cameras| Yes | Yes | Yes | |

<a name=sbig></a>
### SBIG Cameras ###

SBIG cameras only allow a single application at a time to access the camera. If the camera is one of the self-guiding models with a built-in guide camera, then the imaging app controlling the imaging chip will need to provide access to the guide camera. The only app we know of with this capability is Sequence Generator Pro which exposes the internal guide camera to PHD2 as an ASCOM camera.

<a name=qhy></a>
### QHY Cameras ###
QHY camera support in PHD2 is based on a older QHY SDK from 2013. QHY has a new SDK and we have been working on integrating this into PHD2.  When available, the new SDK will support all recent QHY cameras on Windows, OSX and Linux. There is a series of QHY test builds available, please check in the PHD2 forum -- search the forum for QHY Test.
