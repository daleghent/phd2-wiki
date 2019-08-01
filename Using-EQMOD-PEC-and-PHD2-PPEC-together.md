Combining EQMOD with SynScan PPEC and PHD2 Predictive PEC

Steve Bellavia, 8/1/2019

There are threads on all, or portions of this topic already.
 
This is an attempt to put it all together.
 
I will do it in 4 posts:
1. This post, as the introduction and references to other similar CN threads.
2. Summary of Randy Roy's EQMOD-to-PPEC recording method.
3. Running PPEC simultaneously with PHD2 Predictive PEC.
4. Guide logs showing the difference in guiding performance between Predictive PEC and Hysteresis guiding.
 
Other similar CN threads:
[https://www.cloudynights.com/topic/631100-a-well-averaged-smoothed-ppec-curve-with-eq6-r-pro/](https://www.cloudynights.com/topic/631100-a-well-averaged-smoothed-ppec-curve-with-eq6-r-pro/)
[https://www.cloudynights.com/topic/612512-predictive-pec-with-phd2/](https://www.cloudynights.com/topic/612512-predictive-pec-with-phd2/)
[https://www.cloudyni...tive-pec/page-2](https://www.cloudyni...tive-pec/page-2)
[https://www.cloudynights.com/topic/603072-phd2-predictive-pec-it-works/](https://www.cloudynights.com/topic/603072-phd2-predictive-pec-it-works/)

EQ6-R Pro + EQMOD PEC training per Randy Roy (rewritten by Steven Bellavia)
 
1. Set up the mount::
- Polar align
- Face scope South near the Celestial Equator, but avoid a meridian flip for at least an hour
- Calibrate guide camera in PHD2
- Run PHD2  Guiding Assistant for 5 minutes and apply recommendations
- Begin auto-guiding
2. In EQMOD, initiate AUTOPEC recording - choose 5 to 9 cycles for best results
3. Once finished recording AutoPEC, EQMOD will automatically switch to Sidereal + PEC tracking
4. Turn OFF auto-guiding
 
Your mount’s red LED is on constantly.
 
5. Go to the right hand side of The EQMOD menu, in the development area and click record. Your mount starts to flash on and off continuously. This indicates the mount is waiting for the index on the worm to cycle through to its starting position. This can take up to 480 seconds or longer depending on where the index happens to be when you start.
6. Once the index is found, the mount begins to record and the red LED on the mount begins flashing in sequences of 2 flashes. After 480 seconds, the recording is complete and the red LED flashes in sequences of 3 flashes indicating that the mount now has Permanent PEC running.
7. Click the refresh button in EQMOD and it will also tell you that PEC is turned on your mount.
8. Don’t forget to change your tracking in EQMOD back to Sidereal since you no longer want Sidereal + PEC tracking, as the mount is doing that now.
 
This should only have to be done once.  You can use your mount's PPEC for now on.
 
Alternate Method (from unguided PHD2 log files):
 
Replace steps 1 through 4 with:
1. Set up the mount::
- Polar align
- Face scope South near the Celestial Equator, but avoid a meridian flip for at least an hour
2. Start PHD2 and run your mount unguided 5 to 9 cycles, (you want a clean, new PHD2 log file, with a single unguided run only).
    When finished, before closing PHD2, apply a time stamp in EQMOD (not sure if this is necessary ?)
    Close PHD2 (to create a single unguided log file)
3. Open PECPrep, and load the unguided PHD2 log file (this will automatically generate a new file specifically for EQMOD)
    In EQMOD, load and play the file that PECPrep created
4. EQMOD will now switch to Sidereal + PEC tracking
 
Then continue with steps 5 and on.
 
Light summary:
- constant red light - just tracking
- red flash on and off - looking for index (can take one or more worm revs)
- red flash in sequence of 2 flashes - recording PEC
- red flash in sequence of 3 - running PEC

You can run your mount's PPEC and use PHD2 Predctive PEC, simultaneously.
 
I would suggest to NOT enter the worm cycle period as the "kernel" period length for PHD2.  The mount is already doing this.
But what to enter may not be straight-forward.
For my new SkyWatcher EQ6-R Pro, I have a few other periodic motions that show up in the FFT analysis.
 
So my suggestion is to pick the next largest magnitude periodic error, and enter that.
That could be the Transfer gear (367 seconds), or the worm second harmonic (240 seconds), or the transfer gear 2nd harmonic (182 seconds).
Make sure you check "auto-adjust", so it finds the correct period to correct for.
 
The other night I entered 480 seconds.  Within 10 minutes, PHD2 "found" the 367 second period on its own and started to correct for that. (I assume the 480 second period was not prominent, as the PPEC was taking care of it, and hence why I am suggesting to not enter that).
 
That same night I accidentally entered 1480 seconds in PHD2 (I was trying to enter 480 seconds), and it found a 700 second period. It shows up on 5 out of 6 unguided sessions, so I think that is real. My guiding was not as good as when it found the 367 second period, but still better than hysteresis guiding.

![https://www.cloudynights.com/topic/670930-combining-eqmod-with-synscan-ppec-and-phd2-predictive-pec/?p=9543776#](https://www.cloudynights.com/topic/670930-combining-eqmod-with-synscan-ppec-and-phd2-predictive-pec/?p=9543776#)

![https://www.cloudynights.com/uploads/monthly_08_2019/post-227322-0-79859000-1564685792_thumb.jpg](https://www.cloudynights.com/uploads/monthly_08_2019/post-227322-0-79859000-1564685792_thumb.jpg)
 
In my next post, I will show the difference in performance of Hysteresis versus Predictive PEC, when run simultaneously with PPEC. 

