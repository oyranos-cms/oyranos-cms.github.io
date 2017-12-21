---
title: CinePaint
permalink: wiki/CinePaint/
layout: wiki
---

CinePaint became its colour management during the work of Stefan Klein
at the project. It is ICC based. As an offshot the Oyranos project was
started. This page describes CinePaints colour management.

Features
--------

-   display ICC colour correction
-   ICC 16-bit editing
-   32-bit ICC corrected viewing
-   CMYK/Lab/Cineon editing
-   Cineon profiles are available as part of the
    [Oyranos](/wiki/Oyranos "wikilink") project at [Oyranos download
    page](http://www.behrmann.name/index.php?option=com_content&task=view&id=34&Itemid=68#profiles)
-   capablility to show image colours in an 3D colour viewer including
    various gamuts - [ICC
    Examin](http://www.behrmann.name/index.php?option=com_content&task=view&id=32&Itemid=70)
-   littleCMS is a fixed dependency
    [CMM](/wiki/ColourMatchingModuls "wikilink")
-   standard paths: /usr/share/color/icc;~/.color/icc + free selectable
    additional directories
-   preference dialog for default profiles and conversion behaviour
    (target for Oyranos integration)
-   proofing profile per loaded image
-   ICC print separation dialog uses the proofing profile by default
-   OpenEXR &lt;-&gt; ICC conversion roundtripping (solved with lcms on
    the fly profiles)

Investigation
-------------

-   16-bit XYZ editing and displaying
-   print dialog needs system wide colour management
-   inconsitent colour UI for the legacy Gtk1 version (channel names,
    alpha handling, partitial colour space specific dialogs)
-   Cineon -&gt; ICC Layer
-   no tonemapping
-   missed floating point precision colour transforms

Links
-----

-   <http://www.cinepaint.org> - Project page
-   [CinePaintColourManagementUserDocumentation](http://cinepaint.bigasterisk.com/CinePaintColourManagementUserDocumentation) -
    Stefan's documentation
-   [CinePaint - 16-bit imaging. From digital camera to
    print](http://www.behrmann.name/index.php?option=com_weblinks&task=view&catid=67&id=56&Itemid=85) -
    english
-   [CinePaint – 16-bit Bildbearbeitung. Von der Kamera zum
    Druck](http://www.behrmann.name/index.php?option=com_weblinks&task=view&catid=67&id=54&Itemid=86) -
    deutsch

[back -&gt; Applications](/wiki/Applications "wikilink")
