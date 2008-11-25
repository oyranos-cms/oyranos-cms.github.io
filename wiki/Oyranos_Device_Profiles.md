---
title: Oyranos/Device Profiles
permalink: wiki/Oyranos/Device_Profiles/
layout: wiki
---

Currently only monitor profiles are supported on unix X window systems.

The man page for the appropriate command line tool “oyranos-monitor” is
shown below:

`NAME`  
`      oyranos-monitor - Oyranos CMS monitor configuration`  
  
`SYNOPSIS`  
`      oyranos-monitor [-x num -y num  profilename] [-x num -y num] [-b -x num`  
`      -y num] [-e -x num -y num] []`  
  
`DESCRIPTION`  
`      This little programm let you  query  and  set  the  monitor  profile(s)`  
`      within the Oyranos colour management system (CMS).`  
  
`OPTIONS`  
`      -x     get/set the x display position`  
  
`      -y     get/set the y display position`  
  
`      -e     reset the hardware gamma table to the defaults`  
  
`      -b     query the profile name from the Oyranos device profile data base`  
  
`      Set up the X11 server with the Oyranos stored monitor profile`  
  
`EXAMPLES`  
`      Put the following in a setup script like .xinitrc:`  
`             # select a monitor profile, load the binary blob into X and`  
`             # fill the VideoCardGammaTable, if appropriate`  
`             oyranos-monitor`  
  
  
`      Assign a ICC profile to a screen:`  
`             oyranos-monitor -x pos -y pos profilename`  
  
  
`      Reset a screens hardware LUT in order to do a calibration:`  
`             oyranos-monitor -e -x pos -y pos profilename`  
  
  
`      Query the server side, network transparent profile:`  
`             oyranos-monitor -x pos -y pos`  
  
  
`      Query the Oyranos device data base profile on the local computer:`  
`             oyranos-monitor -b -x pos -y pos`  
  
  
`AUTHOR`  
`      Kai-Uwe Behrmann (ku.b (at) gmx.de)`  
  
`SEE ALSO`  
`      oyranos-config-fltk(1) oyranos-policy(1) oyranos(3)`  
` `  
`BUGS`  
`      at: `[`http://sourceforge.net/tracker/?group_id=177017&atid=879553`](http://sourceforge.net/tracker/?group_id=177017&atid=879553)
