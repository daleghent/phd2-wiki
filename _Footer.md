Approach #2: 

(This is from a Paramount ME-II owner using SGP and PHD2 with no issues, including functioning TPoint model and PEC turned on.

1.  In The Sky ASCOM driver I could never get DirectGuide to work and operate correctly, I run with "Enable Tracking Offsets" and "Enable PulseGuide" turned on

2.  For Plate Solving in SGP to work I have the "Sync Behavior" set to "Target Offset" this is necessary to prevent corrupting the TPoint model


Approach #3:

(from another user) Use poth [plain old telescope hub] and then have poth connect to tsx.  Then direct drive worked.


PERMISSIONS NOTE: Some users have reported having intermittent problems, or not seeing the EQMOD ascom options within PHD2. They have reported running all ascom software (including platform, drivers, and software) as Admin corrected these problems. WARNING: PHD and many other software programs recommend against running programs in admin mode as they give elevated priveleges that may not be required. However you approach this, all ascom and related software (and i mean *all* of it) needs to be run with identical user permissions.