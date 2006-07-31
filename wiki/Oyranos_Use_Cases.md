---
title: Oyranos/Use Cases
permalink: wiki/Oyranos/Use_Cases/
layout: wiki
tags:
 - Oyranos
---

Introduction
------------

Oyranos provides many settings, which are not easily to understand
without colour management background. The following Use Cases will
describe practical questions and theyre academic answere by Oyranos.

Home user browser/viewer/print application
------------------------------------------

The user needs some way to copy files from the camera. The application,
lets call it SmartBrowse (SB), must check if a ICC profile is embedded
or if the colorimetric parameters of the colour space are otherwise
specified in the image. This is the image colour space.

If SB cant find one it becomes a bit difficult.

If SB has no information about the camera from a exif tag, but exif is
pretty standard, it should include such information into the loaded
file. In TIFF the model, make and software tags are good candidates to
store such information or add a exif tag, with at least what is
available from loading the images.

Ok, we can not query for the profile elsewhere. SB will ask Oyranos what
to do. To use Oyranos we have to prepare some bits.

### Code Preparation

SB has to put a

`#include `<oyranos/oyranos.h>

in the code, in order to use Oyranos. oyranos-config --cflags delivers
the compiler flags and oyranos-config --ldflags the linker flags.

You can then link Oyranos into your application with:

`` cc `oyranos-config --cflags` `oyranos-config --ldflags` mycode.c -o SB ``

### Behaviour Preferences

As most tasks on the computer make sense by automating many steps to
easen life of the user, Oyranos provides some settings which will route
SB to do its work automatical right. We may aks: What did the user
decide to do in the case of getting untagged data? ... and write:

`int untagged_action = oyGetBehaviour (oyBEHAVIOUR_ACTION_UNTAGGED_ASSIGN );`

With a 0 in untagged\_action nothing needs to be done. The image shall
not be colour corrected further.

With a 1 in untagged\_action the image shall obtain a standard colour
space. We will continue with this case below.

The thierd possibility comes with a 2 in untagged\_action. It means a
dialog shall appear to let the user select a appropriate profile by
himself.

### Standard Profile Preferences

Then SB can ask Oyranos for its default Rgb profile setting. The call:

`char *profile_name = oyGetDefaultProfileName ( oyASSUMED_RGB , myAllocateFunc );`

gives you a profile name.

As a fourth option SB should as well be able to look into a database for
comparing the camera model and possibly serial number with available ICC
profiles for the system, ähhmmm but it is not yet ready in Oyranos.

### Obtaining a Profile

After obtaining the profile name it can be loaded by:

`size_t size;`  
`void *standard_rgb_profile = oyGetProfileBlock (profile_name, &size, myAllocateFunc);`

The next step is to query Oyranos for the display profile as SB want to
show immediately thumbnail images. Here SB source text has to include

`#include `<oyranos/oyranos_monitor.h>

`char *monitor_profile = oyGetMonitorProfile (display_name, &size, myAllocateFunc);`

should deliver the needed bits.

Some important options to pass to your
[ColourMatchingModuls](/wiki/ColourMatchingModuls "wikilink") are queried
now:  
Rendering Intent, Black Point Compensation, possibly a thierd profile -
the proofing profile with its own rendering intent and the option for
marking out of gamut colours.

Thats all information you need to correct the image for displaying on
monitor.

### Printing

For printing in a very simple Home user setup, we see just one printer
and can use the proofing profile as the one default print device
profile. Thats very simple. Ask for the proofing profile and convert the
image from the image colour space to the proofing colour space with the
default intent. Sent the data to the printer driver or create a print
file.

Oyranos Configuration Logic
---------------------------

The \\b oyranos-config-fltk configuration dialog shows clearly, what
options are available and should be considered in a workflow.

|                                                                                |                                                                                                                 |
|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-flu-0.1.5_policy.png "Oyranos-config-flu-0.1.5_policy.png") | Here te user selects the most simple way. He needs to identify her-/himself and choose the appropriate setting. |

The next tab is the paths selection one:  
![](Oyranos-config-flu-0.1.5_paths.png "fig:Oyranos-config-flu-0.1.5_paths.png")

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
