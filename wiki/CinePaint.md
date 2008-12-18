---
title: CinePaint
permalink: wiki/CinePaint/
layout: wiki
tags:
 - Programms
---

CinePaint became its colour management during the work of Stefan Klein
at the project. It is ICC based. As an offshot the Oyranos project was
started to support interapplication conventions for colour management.
This page describes CinePaints colour management.

Features
--------

-   display ICC colour correction
-   preference dialog for default profiles and conversion behaviour
    (target for Oyranos integration)
-   display / editing / assumed input / proofing profile settings
-   profile missmatch behaviour selectable
-   ICC 8/16-bit editing and corrected viewing
-   32-bit HDR colour corrected viewing
-   CMYK/Lab/CineonLog editing
-   Cineon profiles are available as part of the
    [Oyranos](/wiki/Oyranos "wikilink") project at [Oyranos download
    page](http://www.behrmann.name/index.php?option=com_content&task=view&id=34&Itemid=68#profiles)
-   on the fly manipulation (look) profiles assignable and useable for
    conversion
-   film playback with colour correction and effects; slow, needs
    further improvement
-   capablility to show image colours in an 3D colour viewer including
    various gamuts (3D histogram) - [ICC
    Examin](http://www.behrmann.name/index.php?option=com_content&task=view&id=32&Itemid=70)
-   littleCMS is a fixed dependency
    [CMM](/wiki/ColourMatchingModuls "wikilink")
-   standard paths: /usr/share/color/icc;~/.color/icc + free selectable
    additional directories
-   one proofing profile per loaded image
-   ICC print separation dialog uses the proofing profile by default
-   for lcms &gt; 1.15 is Cmyk-&gt;Cmyk black preserving enabled; non
    selectable
-   OpenEXR &lt;-&gt; ICC conversion roundtripping (solved with lcms on
    the fly profiles)
-   BPC is on by default (v0.20-3)
-   Oyranos is the default configurator if available

Investigation
-------------

-   16-bit XYZ editing and displaying
-   print dialog needs system wide colour management
-   inconsitent colour UI for the legacy Gtk1 version (channel names,
    alpha handling, partitial colour space specific dialogs)
-   automate Cineon -&gt; ICC profile selection; currently manual
-   tonemapping
-   missed floating point precision colour transforms

Screenshots
-----------

Note the actual configuration is done in the [Oyranos Configuration
Dialog](/wiki/Oyranos_Configuration_Dialog "wikilink") to adhere to system
wide user settings.

CM Preferences (v0.22-1):

![](Ss_0.22-1_preferences.png "Ss_0.22-1_preferences.png")

CM Preferences without Oyranos (v0.23-0):

![](Cinepaint_screenshot_0.23_en.png "Cinepaint_screenshot_0.23_en.png")

[ICC Examin](/wiki/ICC_Examin "wikilink")'s CinéPaint plug-in showing
collapsing colours of a proofed image:

<http://www.behrmann.name/images/artikel/cinetut/cinepaint_0.23-0_it8_colourvis_hardproof_de.png>

Links
-----

-   <http://www.cinepaint.org> - Project page
-   [CinePaintDocumentation](http://cinepaint.bigasterisk.com/CinePaintDocumentation) -
    Wiki
-   [CinePaintColourManagementUserDocumentation](http://cinepaint.bigasterisk.com/CinePaintColourManagementUserDocumentation) -
    Stefan's documentation
-   [Colour Management and Colour Correction in
    CinePaint](http://www.behrmann.name/index.php?option=com_weblinks&task=view&catid=67&id=137) -
    Stefan Klein; A final year project at the University of Edinburgh
    [short
    html](http://www.inf.ed.ac.uk/undergraduate/projects/stefanklein/)[appendix](http://www.behrmann.name/index.php?option=com_weblinks&task=view&catid=67&id=138)
-   [CinePaint - 16-bit imaging. From digital camera to
    print](http://www.behrmann.name/index.php?option=com_weblinks&task=view&catid=67&id=56&Itemid=85) -
    english
-   [CinePaint – 16-bit Bildbearbeitung. Von der Kamera zum
    Druck](http://www.behrmann.name/index.php?option=com_weblinks&task=view&catid=67&id=54&Itemid=86) -
    deutsch

[back -&gt; Applications](/wiki/Applications "wikilink")
