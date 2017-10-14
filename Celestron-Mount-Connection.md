## Contents ##

* [Basic Connection Info](https://github.com/OpenPHDGuiding/phd2/wiki/Celestron-Mount-Connection/#basic-connection-info)
* [PECTool Connection](https://github.com/OpenPHDGuiding/phd2/wiki/Celestron-Mount-Connection/#pectool-connection)
* [Declination Backlash Info](https://github.com/OpenPHDGuiding/phd2/wiki/Celestron-Mount-Connection/#declination-backlash-info)

## Basic Connection Info ##

From Peter Wolsley: ([PHD2 forum thread](https://groups.google.com/d/msg/open-phd-guiding/h6sLV4ktQL0/D0Q6IYV_AwAJ))

Bharath,

I own a Celestron CGEM 800 and I think I know what your issue is.  It has to do with the purpose of Nexremote and how it conflicts with your handcontroller.  Celestron developed the Nexremote application to be a full replacement of the functionality of your handcontroller. Nexremote is a software emulator of the exact same firmware contained in your hardware handcontroller. This includes alignment and calibration of your CGEM.  A very important conflict needs to be kept in mind. 

If you wish to use the Nexremote app, it will invalidate any alignment/calibration performed with the hardware handcontroller forcing you to align and calibrate your mount using the Nexremote app.  It's almost as if you can only use the hardware handcontroller or Nexremote... never both.
 
So how are you suppose to get everything running correctly?  There are two methods available:  
Let's assume the following:  
Your hardware handcontroller is plugged into your mount and it's serial port cable is plugged into a USB to serial converter.  Your computer says that this USB to serial converter is connected to **COM3**.  When you run Nexremote you have it's virtual port set to **COM4**.
 
#### Method 1...Using only the handcontroller ####
a)Configure the Celestron ASCOM driver COM port to COM3.  
b)Align and Calibrate your mount using the hardware handcontroller.  
c)Align using 2 stars and calibrate using 4 stars.  
d)Polar align (the ASPA method) using the hardware handcontroller.  
e)Start PHD2 and connect your mount using the Celestron Telescope Driver (ASCOM).  

You will now be able to use PHD2. You must NOT use Nexremote while using this method.
 
#### Method 2...Using only the Nexremote app. ####
a)Configure the Celestron ASCOM driver COM port to COM4.  
b)Run the Nexremote App and connect to the mount using COM3.  
c)Align and Calibrate your mount using Nexremote.  
d)Align using 2 stars and calibrate using 4 stars.  
e)Polar align (the ASPA method) using Nexremote.  
f)Start PHD2 and connect your mount using the Celestron Telescope Driver (ASCOM).  

You will now be able to use PHD2. You can only use the slew buttons on the hardware handcontroller (if you wish) when using this method.

I hope this helps

Peter


## PECTool Connection ##

From Peter Wolsley: ([PHD2 forum thread](https://groups.google.com/d/msg/open-phd-guiding/Mymt3H5FLKE/X-Oi7QO1BAAJ))

Mark,
It is a bit of a "can of worms" getting PECTool to work with PHD2.  The problem with PECTool, as I understand it, is that PECtool only has two methods for connecting to your mount.  One is to directly connect to the mount via a com port.  This method totally eliminates the possibility of using ASCOM because the com port to the mount is now dedicated to PECTool and not available to ASCOM.  Only one piece of software can connect to the com port at any time.

There is one "custom" method for keeping both ASCOM and PECTools talking to the mount and that is to introduce NexRemote to the mix.  If you run NexRemote and configure NexRemote to use the mount's com port you can also declare a "virtual com port" and tell ASCOM to use this virtual port.  For this scheme to work you have to also calibrate/align your mount using NexRemote as it completely bypasses your hardware hand controller.  Nexremote is actually a software emulator of your hardware handcontroller and both can't be operated at the same time.  For my CGEM the USB to serial cabling actually plugs into my handcontroller but when using NexRemote I shouldn't touch any of the hardware handcontroller buttons (I can touch the slew buttons but that's all).

That was a messy explaination but now that you are using NexRemote you now have a method for additionally connecting PECTool to your mount.  PECTool has a method called "NexRemote Direct" which utilizes a very custom interface in NexRemote that allows it to communicate with your mount, your ASCOM driver and PECTool simultaneously.  I have used this method several times.
If you don't want to go down this road then you are left with not using ASCOM, or NexRemote when using PECTool.  You simply connect PHD2 to the mount using the "On Camera" method and connect PECTool to the mount's com port.  This is exactly what you have already been doing. There is nothing wrong with this method and nothing wrong with using the PPEC feature of PHD2 while using PECTool.  The reason why is that PECTool is only recording the RAW RA position feedback of your mount and the RA Index.  It does not look at any autoguiding commands. All that is important is that your guiding is good.  If your guiding is all over the map then PECtool is going to blindly record the RA movements and convert them into a PE curve.

Peter

## Declination Backlash Info ##

From Mark: (Forum thread)[https://groups.google.com/d/topic/open-phd-guiding/8Eb_TCTeaVg/discussion]

Hi Group,
my mount is new, purchased in January of this year.  It features the spring loaded DEC and RA drives, and is likely the last iteration by Celestron.  I raised a question to their tech group about reducing DEC backlash, specifically with the mechanical adjustments.  The following is their partial response and deals strictly with using the softwares to mitigate the backlash.  While not what I was looking for, it appears to be a thoughtful response.

QUOTE FROM CELESTRON:

"We consider acceptable backlash to be within 3 seconds of delay when reversing directions at rate 3. Rate 3 is 4x sidereal speed. Of course this will translate into a very long delay when autoguiding at ½ sidereal.

Concerning ½ sidereal speed for autoguiding:
The default guide rate is set to ½ sidereal which in most cases is too slow. This is further compounded by the existing backlash, which explains why PHD2 reports such a large amount of Dec backlash. There are 3 ways to combat this before making any mechanical adjustment:

1\.      Adjust the autoguide rate in the NexStar+ hand control from 50 (default) to 99 for R.A. and especially Dec. This will double the autoguide speed, making autoguide movements much more responsive. Auto guide aggression rates can always be changed in PHD2 while guiding, so it’s better to start with the maximum responsiveness.

2\.      Despite the suggested calibration step size in PHD2, increase the calibration step 50% or so. For example, if it was 100ms, increase to 150ms. This will cause larger movements to help complete the calibration process. Otherwise, PHD2 may iterate 20, 30 or more calibration steps in Dec which can make for a messy calibration. If the steps are too large it can be toned down later.

3\.      Finally, identify which direction the Dec drift is in. This can be done by turning Dec aggression to 0 while guiding, or running the drift align procedure in PHD2. Once you identify which direction Dec is drifting in, disengage Dec guiding in the other direction (in the “brain” advanced settings of PHD2). Once you do this, Dec backlash no longer becomes a factor. Unless polar alignment is absolutely perfect, we will see a trend in Dec drift. This is actually advantageous so that we can keep Dec moving to one side of the gear backlash. ".

END QUOTE

Thanks,
Mark
