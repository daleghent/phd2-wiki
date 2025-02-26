This page describes how to set up a build environment from scratch on MS-Windows to compile and run PHD2.

# Summary #

  1. Get the Visual Studio C++ compiler
  1. Install Visual Leak Detector
  1. Install wxWidgets
  1. Install fitsio
  1. Install opencv
  1. Get PHD2 sources
  1. Compile PHD2
  1. Running PHD2 from Visual Studio

# Step-by-step #

1. If you do not yet have a version of Visual Studio 2013 for Windows Desktop then get a free copy at

http://www.visualstudio.com/en-us/downloads

The download you want is "Visual Studio Express 2013 for Windows Desktop".

Visual Studio 2013 requires Windows 7 SP1 or later; it will not install on Windows XP.

2. Download and install Visual Leak Detector (VLD) Version 2.3.0 from https://vld.codeplex.com/

The VC++ project files assume you have VLD installed in the default
location:

> c:\program files (x86)\visual leak detector\

so make sure you install it there.

> _Extra Info_ The VLD is packaged as a Windows installer exe file, so just run it. It will ask if you want to automatically add its directory into the PATH environment string, and you should answer ‘yes.’

3. Download wxWidgets 3.0.2 from
> http://sourceforge.net/projects/wxwindows/files/

In order to get a static copy of wx working, you need to build it yourself.

Install it in <wx install path>, and cd into the build directory:

> cd <wx install path>\build\msw

The following step might not be needed, at least not on WinXP.

Load the VC variables so nmake and the command line compilers are in the path:

> "\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\vcvars32.bat"

Do two command line builds, one for release, one for debug:

```
  nmake -f makefile.vc BUILD=release SHARED=0
  nmake -f makefile.vc BUILD=debug SHARED=0
```

Set a WXWIN environment variable to point to <wx install path> so that the PHD2 build will find the bits.

> _Extra Info_ wxWidgets sources are downloaded as a zip file. You should stick with the 3.0.2 release used in the current PHD2 build. On the wxWidgets site, go to the downloads page, then select ‘releases’ at the upper left to find the earlier release package you need.  Once it’s downloaded, extract into a location you want.

> You will probably need to load the VC variables on Win 7, as described above, before you can run the ‘nmake’ commands.  You must run vcvars32.bat and do the nmake runs in a single command-line session or the VC environment variables won’t be retained.  Just go into the \build\msw directory and run the \Program Files (x86)… vcvars32.bat file from  there.  You can use the tab key to reduce the amount of typing required. Then set the WXWIN environment variable as follows:  suppose you’ve installed wxWidgets in a folder c:\dev\CPP\_Libs\wxWidgets-3.0.2\.  Then the environment variable should look like this:

> WXWIN = C:\dev\CPP\_Libs\wxWidgets-3.0.2\

4. Download the CFITSIO V3.340 Software Library from

> http://heasarc.gsfc.nasa.gov/fitsio/

or

> [ftp://heasarc.gsfc.nasa.gov/software/fitsio/c/cfit3340.zip](ftp://heasarc.gsfc.nasa.gov/software/fitsio/c/cfit3340.zip)

Extract in <fits location>

Set an environment variable CFITSIO to <fits location>

> _Extra Info_ The latest Windows zip file for CFITSIO does not have pre-compiled versions of the libraries needed by PHD2.  So you will need to build them in much the same way as you built the wxWidgets files.  From a single command-line session, run the same "\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\vcvars32.bat" file, cd to the <fits location> install directory, then run two nmakes:
```
nmake winDumpExts.mak
nmake makefile.vcc
```

> You should ignore all the warning messages.  These steps are described in README.win32 in the CFITSIO directory – just open it with a text editor.

5. Download the pre-built OpenCV 2.4.5 DLLs from http://openphdguiding.org/opencv-245-vc12.zip. Unzip and install in <opencv location>. Set the environment variable OPENCV\_DIR to point to the <opencv location>\install. For example, if you installed the folder to C:\opencv-245-vc12, then set OPENCV\_DIR to "C:\opencv-245-vc12\install".

Note: do not install the prebuilt DLLs from the opencv distribution from opencv.org. These were built with VS 2010 and will introduce an unwanted dependency on the VS 2010 C++ runtime DLLs.  If you do prefer to download opencv from opencv.org, make sure you re-build it with VS 2013.

Next you will have to copy 3 Debug and Release DLLs from <opencv location>\install\x86\vc12\bin\

The files you need to copy are:

```
Debug: opencv_core245d.dll opencv_highgui245d.dll opencv_imgproc245d.dll
Release: opencv_core245.dll opencv_highgui245.dll opencv_imgproc245.dll
```

You can either copy these to the Debug\ and Release\ build directories that VC creates, or copy them to an existing PHD2 install directory. If you copy them to the PHD2 install directory, make sure that directory is in your PATH environment variable. (See note below "Running PHD2 from Visual Studio".)

> _Extra Info_ PHD2 is currently using OpenCV version 2.4.5, but this is no longer the latest OpenCV release.  Don’t download and install the latest release – stick with the version used by the PHD2 build.  The version numbers are embedded in the OpenCV filenames, so PHD2 is implicitly tied to a specific release level.

6. Get PHD2 sources from the trunk branch at

> http://code.google.com/p/open-phd-guiding/

7. Open phd2.sln in Visual Studio, select the Release or Debug build target and build.

> _Extra Info_ You may have jumped ahead at some point and downloaded the PHD2 source just for inspection.  If you opened the VCC project before doing all of the steps above, you will obviously see a ton of IntelliSense syntax errors.  These may persist even after you’ve done the steps above and even after you’ve successfully compiled the project.  You have two options at this point: you can try to sort through the IntelliSense options and somehow get it to rebuild its database or you can delete the PHD2 files and simply download them again.  The second option seems a lot easier.  If you’ve set everything up as described, the project will compile and you are good to go.

8. Running PHD2 from Visual Studio

PHD2 has runtime dependencies on several camera support libraries (DLLs). In order to run, the DLLs must be available either in a directory on PATH (environment variable), or in the same directory as PHD2.exe.

One solution is to download and install an official PHD2 release build, and then add the install location to the PATH environment variable.

An alternate approach is to manually copy cfitsio.dll and the DLLs from WinLibs\ to the Release\ and Debug\ directories.

Once you do one of those steps, you should be able to run PHD2 from Visual Studio.