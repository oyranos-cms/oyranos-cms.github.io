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
or otherwise is specified in the image. This is the starting colour
space.

If SB cant find one it becomes a bit difficult. Now SB should look ito a
database for comparing the camera model and possibly serial number with
available ICC profiles for the system, ähhmmm not yet ready in Oyranos.

If SB has no information about the camera from a exif tag, beside this
exif is pretty standard, it should include such information into the
loaded file. In TIFF the model, make and software tags are good
candiates to store such information or add a exif tag with at least what
is available from loading the images.

Ok, we can not query for the profile elsewhere. SB will ask Oyranos what
to do. To use Oyranos we have to prepare some bits.

SB has to put a

`#include `<oyranos/oyranos.h>

in the code, in order to use Oyranos. oyranos-config --cflags delivers
the compiler flags and oyranos-config --ldflags the linker flags.

You can then link Oyranos into your application with:

`` cc `oyranos-config --cflags` `oyranos-config --ldflags` mycode.c -o SB ``

As most tasks on the computer make sense by automating many steps to
easen life of the user, Oyranos provides some settings which will route
SB to do the right. We may aks: What did the user decide to do in the
case of getting untagged data? ... or write:

`int untagged_action = oyGetBehaviour (oyBEHAVIOUR_ACTION_UNTAGGED_ASSIGN );`

Falls untagged\_action 0 ergibt geschiet nichts. Das Bild wird
unkorrigiert dargestellt.

With a 1 in untagged\_action the image shall obtain a standard colour
space. We will continue with this case below.

The thierd possibility comes with a 2 in untagged\_action. This means a
dialog shall appear to let the user select a appropriate profile by
himself.

Then SB can ask Oyranos for its default Rgb profile setting. The call:

`char *profile_name = oyGetDefaultProfileName ( oyASSUMED_RGB , myAllocateFunc );`

gives you a profile name which can be loaded by:

`size_t size;`  
`void *standard_rgb_profile = oyGetProfileBlock (profile_name, &size, myAllocateFunc);`

The next step is to query Oyranos for the display profile as SB want to
show immediately thumbnail images. Here SB source text has to include

`#include `<oyranos/oyranos_monitor.h>

`char *monitor_profile = oyGetMonitorProfile (display_name, &size, myAllocateFunc);`

should deliver the needed bits.

Some important option to pass to you
[ColourMatchingModuls](/wiki/ColourMatchingModuls "wikilink") are queried
now:  
Rendering Intent, Black Point Compensation, possibly a thierd profile -
the proofing profile with its own rendering intent and the option for
marking out of gamut colours.

Thats all information you need to correct the image for displaying on
monitor.

Oyranos Configuration
---------------------

<http://www.oyranos.org/images/oyranos-config-fltk-0.1.5_2.png>

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
