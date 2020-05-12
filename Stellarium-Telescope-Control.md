**Update May 2020**
As of Stellarium v0.19.3, the TelescopeControl plugin now supports ASCOM.

Stellarium is free, open-source planetarium that runs on a variety of platforms.  It appears to be primarily focused on providing rich, realistic visualization tools for the night sky along with extensive catalogs of deep-sky objects.  Stellarium includes a ‘TelescopeControl’ plug-in that supports slewing for a set of commonly used telescopes.  Regrettably, the plug-in doesn’t support pulse-guiding nor does it use ASCOM (or INDI) standards.  Consequently, the Stellarium connection to the mount can’t be shared with other apps, and PHD2 can’t connect to the mount if the Stellarium TelescopeControl plug-in is being used.  Fortunately, the plug-in interface is public and third-party developers can write their own plug-ins.  One of these, StellariumScope, lets Stellarium use an ASCOM mount connection for its telescope functions.  More importantly, this also allows PHD2 and other astronomy applications to share the connection to the mount. 

At the present time (Feb 2018), the StellariumScope plug-in isn’t distributed as part of the general release so it must be downloaded and installed separately.  The Stellarium WIKI includes a current list of telescope control plug-ins:
http://stellarium.sourceforge.net/wiki/index.php/Main_Page
http://stellarium.sourceforge.net/wiki/index.php/Telescope_Control

The StellariumScope plug-in entry includes a link to the web site hosted by the plug-in author with installation and use guides.
