### PHD2 and Guiding a Paramount

Software Bisque doesn’t provide ASCOM interfaces to their mounts without a little extra work on your part.  You first need to install their plug-in, called the ASCOM 2x Mount Adaptor:

[https://ascom-standards.org/Downloads/ScopeDrivers.htm#Bisque2x](https://ascom-standards.org/Downloads/ScopeDrivers.htm#Bisque2x)

When you connect to that, you then need to make sure the settings match these:

![](https://openphdguiding.org/TSX_Ascom_Parameters.jpg)

The important settings here are ‘use DirectGuide’ and ‘Can Get Pointing State’

You must be running TheSkyX for any of this to work - the 2x Mount Adaptor is simply translating ASCOM mount commands into SB scripting commands that are sent to TheSkyX.  This means that scripting must also be enabled in TheSkyX, which evidently requires it to be run **once-only** in Administrative mode. Once you have enabled scripting, exit TheSkyX and don't run it again in Administrative mode.  Doing so will create problems for any ASCOM applications that want to access the mount.  When you are ready to connect to the mount, use TheSkyX user interface to choose from the list of ASCOM mount drivers, that's where you'll see the 2x Mount Adaptor - you can't just connect to their own (native) Paramount driver.  This should all be a one-time exercise - once PHD2 has connected to the mount, it will remember which mount driver to use.