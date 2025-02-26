# PHD Socket Server Interface #

PHD supports control and monitoring through its _Socket Server_ interface.

> Note: using the socket server for status monitoring has been superseded by the EventMonitoring interface which provides much more detailed status information.

When the server is enabled (Tools -> Enable Server), PHD2 listens for TCP connections on port 4300. It accepts one-byte commands and sends one-byte responses. PHD2 supports multiple concurrent client connections. When there are multiple PHD2 instances, each instance listens on successive TCP port numbers (4301, 4302, ...).

The available commands are given in the table below. The command and response are each a single byte with the indicated values.

| **Command name** | **Value** | **Description** | **Response** |
|:-----------------|:----------|:----------------|:-------------|
| MSG\_PAUSE       | 1         | Pause guiding. Camera exposures continue to loop if they are already looping.| 0            |
| MSG\_RESUME      | 2         | Resume guiding if it was paused, otherwise no effect.| 0            |
| MSG\_MOVE1       | 3         | Dither a random amount, up to +/- 0.5 x dither\_scale |  Camera exposure time in seconds, but not less than 1 |
| MSG\_MOVE2       | 4         | Dither a random amount, up to +/- 1.0 x dither\_scale| Camera exposure time in seconds, but not less than 1 |
| MSG\_MOVE3       | 5         | Dither a random amount, up to +/- 2.0 x dither\_scale| Camera exposure time in seconds, but not less than 1 |
| MSG\_IMAGE       | 6         | (not currently implemented in PHD2) | 1            |
| MSG\_GUIDE       | 7         | (not currently implemented in PHD2)| 1            |
| MSG\_CAMCONNECT  | 8         | (not currently implemented in PHD2)| 1            |
| MSG\_CAMDISCONNECT | 9         | (not currently implemented in PHD2)| 1            |
| MSG\_REQDIST     | 10        | Request guide error distance| The current guide error distance in units of 1/100 pixel. Values > 255 are reported as 255. |
| MSG\_REQFRAME    | 11        | (not currently implemented in PHD2)| 1            |
| MSG\_MOVE4       | 12        | Dither a random amount, up to +/- 3.0 x dither\_scale| Camera exposure time in seconds, but not less than 1 |
| MSG\_MOVE5       | 13        | Dither a random amount, up to +/- 5.0 x dither\_scale| Camera exposure time in seconds, but not less than 1 |
| MSG\_AUTOFINDSTAR | 14        | Auto-select a guide star. | 1 if a star was selected, 0 if not |
| MSG\_SETLOCKPOSITION | 15        | Read 2 16-bit integers, x and y,from the socket and set the lock position to (x,y) | 0            |
| MSG\_FLIPRACAL   | 16        | Flip RA calibration data | 1 if RA calibration data was flipped, 0 otherwise|
| MSG\_GETSTATUS   | 17        | Get a value describing the state of PHD | 0: not paused, looping, or guiding <br> 1: capture active and star selected <br> 2: calibrating <br> 3: guiding and locked on star <br> 4: guiding but star lost <br> 100: paused <br> 101: looping but no star selected
| MSG_STOP         | 18        | Stop looping exposures or guiding| 0. Client should poll with MSG_GETSTATUS to check that looping/guiding has actually stopped.|
| MSG_LOOP         | 19        | Start looping exposures|0 if request to start looping was accepted, non-zero otherwise (like when looping was already active). Client should poll with MSG_GETSTATUS to see if looping actually started. |
| MSG_STARTGUIDING | 20        |Start guiding    | 0. Client should poll with MSG_GETSTATUS to check that guiding has actually started.|
| MSG_LOOPFRAMECOUNT | 21        |Get the current frame counter value.| 0 if not looping or guiding. Otherwise, the current frame counter value (capped at 255). The frame counter is incremented for each camera exposure when looping or guiding.|
| MSG_CLEARCAL     | 22        |Clear calibration data (force re-calibration) | 0            |
| MSG_FLIP_SIM_CAMERA | 23        | When the camera simulator is active, simulate a scope meridian flip|0             |
| MSG_DESELECT     | 24        | De-select the currently selected guide star. If subframes are enabled, switch to full frames. This command should be sent before sending MSG_AUTOFINDSTAR to ensure a full frame is captured. For example, the following sequence could be used to select a guide star: MSG_STOP, MSG_DESELECT, MSG_LOOP, MSG_LOOPFRAMECOUNT, MSG_AUTOFINDSTAR. | 0            |
|                  | <any other value> | unknown command | 1            |
