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
describe practical questions and they're academic answer by Oyranos.

Home user browser/viewer/print application
------------------------------------------

The user needs some way to copy files from the camera. The application,
lets call it SmartBrowse (SB), must check if a ICC profile is embedded
or if the colorimetric parameters of the colour space are otherwise
specified in the image. This is the image colour space.

In detail this is:

-   the embedded profile, if it is not available ask for
-   the EXIF tag and look at the colour space, or
-   other colorimetric information (e.g. Tiff IFD or OpenEXR headers
    with colorimetric parts)

If SB cant find the desired information in the image it becomes a bit
uncertain.

The next is to query a hardware database. If SB has no information about
the camera from an EXIF tag, but EXIF is pretty standard, it should
include such information into the loaded file. In TIFF the model, make
and software tags are good candidates to store such information or add
an EXIF tag, with at least what is available from loading the images.

SB should as well be able to look into a common hardware database for
comparing the camera model and possibly serial number with available ICC
profiles for the system, ahhemmm but it is not yet ready in Oyranos.

In case no profile is returned, SB will ask Oyranos what to do next. To
use Oyranos we have to prepare some bits.

![](CMS_Linux2-6.0.png "CMS_Linux2-6.0.png")

### Code Preparation

SB has to put a

`#include <oyranos.h>`

in the code, in order to use Oyranos. oyranos-config --cflags delivers
the compiler flags and oyranos-config --ldflags the linker flags. Or use
pkg-config if installed.

You can then link Oyranos into your application with:

`` cc `oyranos-config --cflags` `oyranos-config --ldflags` mycode.c -o SB ``

### Behaviour Preferences

As most tasks on the computer make sense by automating many steps to
ease life of the user, Oyranos provides some settings, which will route
SB to do its work automatically right. We may ask: what did the user
decide to do in the case of getting untagged data? ... and write:

`int untagged_action = oyGetBehaviour (oyBEHAVIOUR_ACTION_UNTAGGED_ASSIGN );`

![](Oyranos-config-flu-0.1.5_behaviour-mismatching_no-image-profile-opt.png "Oyranos-config-flu-0.1.5_behaviour-mismatching_no-image-profile-opt.png")

With a 0 in untagged\_action nothing needs to be done. The image shall
not be colour corrected further.

With a 1 in untagged\_action the image shall obtain a standard colour
space. We will continue with this case below.

The third possibility comes with a 2 in untagged\_action. It means a
dialog shall popup to let the user select a appropriate profile by
himself.

### Standard Profile Preferences

Then SB can ask Oyranos for its default RGB profile setting. The call
does this:

`char *profile_name = oyGetDefaultProfileName ( oyASSUMED_RGB , myAllocateFunc );`

### Obtaining a Profile

After obtaining the profile name it can be loaded by:

`size_t size;`  
`void *standard_rgb_profile = oyGetProfileBlock (profile_name, &size, myAllocateFunc);`

The next step is to query Oyranos for the display profile as SB want to
show immediately thumbnail images. Here SB source text can include

`#include `<oyranos/oyranos_monitor.h>

`char *monitor_profile = oyGetMonitorProfile (display_name, &size, myAllocateFunc);`

should deliver the needed bits.

Some important options to pass to your
[ColourMatchingModuls](/wiki/ColourMatchingModuls "wikilink") are queried
now:  
Rendering Intent, Black Point Compensation, possibly a third profile —
the proofing profile with its own rendering intent and the option for
marking out of gamut colours.

Neutral gray is recommended as the out of gamut colour. Areas marked
with gray show a good contrast to any strong saturated colour, which may
fall out of gamut.

That's all information you need to correct the image for displaying on
monitor.

### Printing

For printing in a very simple Home user setup, we see just one printer
and can use the proofing profile as the one default print device
profile. That's very simple. Ask for the proofing profile and convert
the image from the image colour space to the proofing colour space with
the default intent. Sent the data to the printer driver or create a
print file.

Image editor
------------

In version 2.0 of SB the capability to edit and save images is
introduced. The new application should behave on loading images the same
as before regarding colour management.

### Less is More

At time of been asked for editing the image, the original colour space
may be exchanged depending on options in Oyranos. This late conversion
shall ensure no unnecessary conversion is done. Marti Maria, the author
of the LittleCMS color engine, likes to point out that colour transforms
are a lossy action, which can, while happen often, decrease the quality.
This should be expected especially for 8-bit per colour channel
representations.

### Editing Colour Space Concept

What is needed is to circumvent the native device colour spaces. They
are often bumby and have strange gray behaviour. Thats' what the device
profiles are for — to eliminate such unevenness in a devices colour
space.

For editing the gray level should stay equal if changing for instance in
RGB all tree channels at the same factor. Therefore in Oyranos exist
beside the Assumed Profiles the Editing Profiles.

All behaves in SB v2.0 the same as before. But when the user wants to
adjust some curves in the new SB he will probably do it on in the
Editing colour space. The Editing colour space is as well known as
workspace.

The appropriate profile is queried with:

`char *profile_name = oyGetDefaultProfileName ( oyEDITING_RGB , myAllocateFunc );`

for editing in Rgb.

### Convert on Mismatch Behaviour

SB should now compare the image colour space, as described in the
previous SB version, with the Editing colour space. If they are equal
all is ok and editing can begin. If not the
oyBEHAVIOUR\_ACTION\_OPEN\_MISMATCH\_RGB behaviour should be asked what
to do.

![](Oyranos-config-flu-0.1.5_behaviour-mismatching_on-rgb-mismatch-opt.png "Oyranos-config-flu-0.1.5_behaviour-mismatching_on-rgb-mismatch-opt.png")

Obtaining 0 means no conversion shall occur and the image profile
remains unchanged.

1 means the conversion to the Editing RGB Colour Space shall be done
automatically without asking further.

2 means pop-up a dialog for presenting alternative colour spaces for
converting to. The oyEDITING\_RGB can be preselected.

For the choices 1 and 2 SB needs to convert to the corresponding colour
spaces. For the dialog SB can either integrate the usual rendering
options (oyBEHAVIOUR\_RENDERING\_INTENT, oyBEHAVIOUR\_RENDERING\_BPC)
with the Oyranos defaults preselected or just use them without further
question.

The image is now ready for editing.

Afterwards the edited image can be shown on screen and printed as in the
pure viewer version of SB.

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
