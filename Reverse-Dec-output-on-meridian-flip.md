PHD2's _Reverse Dec output after meridian flip_ setting depends on the mount model.  Here are the mounts that we know about.

If your mount is missing from the list, please run the Meridian Flip Calibration Tool (Tools > Calibrate meridian flip) and report your result in the [PHD2 Forum](https://groups.google.com/forum/?fromgroups=#!forum/open-phd-guiding).

|Mount Manufacturer|Mount Model|Reverse dec output needed|Notes|
|----|----|:----:|----|
|Astro-Physics|Any|No||
|Celestron|Any|No|Confirmed for CGX, CGE and CGE Pro models, probably the same for all mounts with the Nexstar+ hand control|
|iOptron|Any|No|ASCOM Driver 5.62 does not report side of pier; version 5.63 is OK<br>mounts confirmed: CEM60, CEM120|
|INDI - EQMOD|Any|No||
|EQMOD - ASCOM|Any|No||
|Losmandy|Gemini-2|No||
|Software Bisque|Any|**YES**||
|Takahashi|Any|No|confirmed for EM-400 with the TemmaLite v6.2.4 driver|
