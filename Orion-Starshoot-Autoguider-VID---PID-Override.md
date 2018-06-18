Apparently some SSAG cameras are susceptible to firmware corruption that causes them to report spurious USB VID/PID values making them show up as an unrecognized USB device.  More info: https://groups.google.com/d/msg/open-phd-guiding/vuwldbOc9OQ/M34xYtJRAgAJ

If your SSAG has this problem, you can workaround the issue so that PHD2 can still access the camera.

For Windows, see the instructions here: https://www.cloudynights.com/topic/406237-orion-ssag-firmware-reset/

For Mac:

Open System Information, find the camera in the USB devices list, and make note of the Vendor Id (VID) and Product Id (PID) values

![](https://openphdguiding.org/ssag_vid_pid_1.png)

Click the camera settings button

![](https://openphdguiding.org/ssag_vid_pid_2.png)

Enter the VID / PID values you found in System Information

![](https://openphdguiding.org/ssag_vid_pid_3.png)

You can now connect to the camera.
