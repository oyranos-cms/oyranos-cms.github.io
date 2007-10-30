---
title: Oyranos/FeatureWish
permalink: wiki/Oyranos/FeatureWish/
layout: wiki
tags:
 - Oyranos
---

Feature Wishes for [Oyranos](/wiki/Oyranos "wikilink")
------------------------------------------------

They come often from discussions at the [OpenICC](/wiki/OpenICC "wikilink")
email list. It is a good place to annotate, suggest, or ask. Writing
here is better than forget elsewhere.

### Devices

-   implement [Device\_Settings](/wiki/Device_Settings "wikilink") in ICC
    profiles

#### Monitor

-   check for validity of a display setup (calibrated: yes/no, expired,
    ...)
-   add non EDID monitor support - by a mix of X description and by
    Xinerama geometry (prepared for 0.1.8)

|     |                         |               |                   |                               |
|-----|-------------------------|---------------|-------------------|-------------------------------|
|     | Progress: 100% \[done\] | Target: 0.1.8 | Start: 2007.08.00 | Assigned to: Kai-Uwe Behrmann |
||

-   common screen naming sheme for X11, osX and Windows
-   [Named Colours](#Named_Colours "wikilink") in X11, osX ,Windows
    representation
-   clear about VCGT handling, use Xcalib (licensing?) or ArgyllCMS,
    give at least a hint at configure time “found Xcalib/Argyll - can
    load VCGT”

### ICC profile handling

-   check for well behaving of Editing colour spaces (Matrix, RGB: gamma
    equally over all channels, Gray axis, ...)
-   check ICC profiles

|              |                |             |                               |
|--------------|----------------|-------------|-------------------------------|
| Progress 10% | Version: x.x.x | Start: 2006 | Assigned to: Kai-Uwe Behrmann |
||

### Settings and Policies

-   use of standard folders for: display profiles, RGB editing profiles,
    CMYK editing profiles.

If advanced users want to use special profiles e.g. for editing, they
have manually to add the profile to this folder. This is an easy way to
implement a solution, that beginners are not able to choose wrong
profiles by accident.

-   color management policies

|              |                |             |                               |
|--------------|----------------|-------------|-------------------------------|
| Progress 70% | Version: 0.1.x | Start: 2004 | Assigned to: Kai-Uwe Behrmann |
||

-   -   done (only allow flat color documents or allow mixed mode
        documents ?)
    -   done (how to deal with profile mismatches during opening files
        ?)
    -   done (how to deal with profile mismatches during placing content
        ?)

-   to add:
    -   done (add CMYK editing profile
        (OY\_DEFAULT\_EDITING\_CMYK\_PROFILE))
    -   done (add non-editable web colour space sRGB for displaying -
        should be used during download from web
        (OY\_DEFAULT\_WEB\_PROFILE=sRGB))
    -   done (profile assigning for untagged data during opening (auto /
        leave / ask) (OY\_UNTAGGED\_ASSIGN\_ACTION))
    -   done (add RGB/CMYK opening mismatch policy (convert / leave
        attached profile/pop-up) , in an pure sRGB environment it could
        be used to make all unknown RGB content equal
        (OY\_MISMATCH\_RGB\_OPEN\_ACTION ...))
    -   done (profile assigning for mismatched data during editing
        policy, harmonise during editing for homogeneous colour space
        documents (OY\_MISMATCH\_CMYK\_CHANGE\_ACTION ...))
    -   note: placing and editing files could equal react regarding
        mismatch (handles the mismatch question from above)
    -   mixed colour space documents for internet warning/quiet
        (OY\_MIXED\_COLOUR\_INTERNET\_DOCUMENT\_WARNING)

<!-- -->

-   rendering intent (Craig Ringer's suggestion)
    -   Perceptual
    -   Relative Colorimetric with BPC
    -   -- Rarely Needed --
    -   Relative Colorimetric without BPC
    -   Absolute Colorimetric
    -   Saturation

<!-- -->

-   allow non persistent settings, examples:
    -   useful for temporarily adding profile paths in osX bundles
    -   switching default profiles to gamma 1.0 versions in one
        application, without touching other applications

#### Directory Paths

-   [ICC profile path
    specification](/wiki/OpenIccDirectoryProposal "wikilink")

|               |                |                     |                   |
|---------------|----------------|---------------------|-------------------|
| Progress: 75% | Version: x.x.x | Start: defacto 2004 | Assigned to: open |
||

-   ICC\_PROFILE\_PATH ? how to interact with Oyranos
-   update Oyranos' internal path representation to the [OpenICC
    Directory Proposal](/wiki/OpenIccDirectoryProposal "wikilink")

### Standard Profiles

-   naming of ECI profiles to something FOGRA corresponding (Chris
    Murphy and others on OpenICC)

|              |                                            |        |                               |
|--------------|--------------------------------------------|--------|-------------------------------|
| Progress: 0% | Version: [0.1.8](#Target_0.1.8 "wikilink") | Start: | Assigned to: Kai-Uwe Behrmann |
||

### CMM Framework

-   backend API a typical CMM should provide

|     |              |                |             |                       |
|-----|--------------|----------------|-------------|-----------------------|
|     | Progress: 0% | Version: x.x.x | Start: 2007 | Assigned to: Scribus? |
||

-   -   transform caching (file format)

-   frontend API, transforms, caching, image description - buffer layout
    / screen position

|     |              |                |             |                               |
|-----|--------------|----------------|-------------|-------------------------------|
|     | Progress: 5% | Version: 1.x.x | Start: 2007 | Assigned to: Kai-Uwe Behrmann |
||

-   -   options handling (xml, GUI)
        -   options should be displayed to users according to
            preferences (for instance [mismatch
            option](/wiki/Oyranos_Configuration_Dialog#Colour_Space_Mismatch "wikilink"))

|     |               |                |             |                               |
|-----|---------------|----------------|-------------|-------------------------------|
|     | Progress: 20% | Version: x.x.x | Start: 2006 | Assigned to: Kai-Uwe Behrmann |
||

-   file support (tiff,png,jpeg), move from Colori

|     |               |                              |                   |                               |
|-----|---------------|------------------------------|-------------------|-------------------------------|
|     | Progress: 25% | Version: first use in Colori | Start: 2007-09-10 | Assigned to: Kai-Uwe Behrmann |
||

### Named Colour

-   colour information structure

|               |                                        |                   |                               |
|---------------|----------------------------------------|-------------------|-------------------------------|
| Progress: 30% | Version: first use in ICC Examin v0.45 | Start: 2007-09-03 | Assigned to: Kai-Uwe Behrmann |
||

Constitute a colour patch presentation:

-   done - CIELab representation
-   done - arbitrary channels (32)
-   done - channel characterisation (4 byte ICC signature)
-   done - channel names list
-   done - colour name
-   done - colour description
-   done - colour nick name
-   done - colour reference (ICC profile)
-   done - cgats representation, this can contain additional observer
    characteristics or spectral data
-   current state is shown
    [here](http://www.behrmann.name/wind/oyranos/icc_examin_2007.09.24.html)
-   done - allow for grouping ( swatches )
-   exchange as colour selection(s) in X11, Quartz ...
-   Named Colours as file (xml?)
-   keep in sync with
    [Create](http://create.freedesktop.org/wiki/index.php?title=Swatches_-_colour_file_format)
-   HDR range information
-   creator signature?
-   gamut warning with the device, which is exceeded - monitor, printer,
    colour space
-   to sRGB float conversion from Lab(D50)/XYZ or from channels over ICC
    profile with lcms
-   gamma handling?

### Miscellaneous

-   done (split Oyranos headers for users, configuration)
-   done (show in headers only stable functions)
-   done (remove unstable functions from descriptions)

<!-- -->

-   later show only advanced options to those users who like it
    -   something like default settings / policy
    -   and modify policy, advanced or custom

<!-- -->

-   done(v0.1.5) Bob Friesenhahn suggested Oyranos should be completely
    relocatable
-   publicate Colori

Todo
----

[Oyranos](/wiki/Oyranos "wikilink") Roadmap

### Target 1.0.0

-   see [inline](http://www.oyranos.org/doc/html/concept_1.0.html)
    documentation

### Target 0.1.8

-   error handling
-   information callback function:

` int (*callback)(int code, const char* format, ...)`

-   -   internally all can stay with macros

-   override default settings, dependent whether they are inbuild or
    explicitely set by a user
    [1](http://www.behrmann.name/wind/cinepaint/cinepaint_2007.04.13_1.html)
-   gray profile setting, done for 0.1.8
-   license change as [stated](http://www.oyranos.org/#license)
-   new default profiles from
    [ECI](http://www.eci.org/eci/de/060_downloads.php)
-   investigate in ColorSync ignoring some CMM:SGI marked profiles

### External

-   [Fedora bug
    entry](https://bugzilla.redhat.com/show_bug.cgi?id=239936)

[--&gt; back to Oyranos wiki](/wiki/Oyranos "wikilink")
