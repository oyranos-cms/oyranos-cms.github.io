---
title: Oyranos/FeatureWish
permalink: wiki/Oyranos/FeatureWish/
layout: wiki
tags:
 - Oyranos
---

Feature Wishes for [Oyranos](/wiki/Oyranos "wikilink")
------------------------------------------------

The assignment of items to a person does not mean there happens
currently work. So offering help is better than waiting with a item of
interest.

A closely related source for project ideas is the *Google Summer of
Code* [wiki page of
OpenICC](http://www.freedesktop.org/wiki/OpenIcc/GoogleSoC2009).

### Devices

-   (done as pddt) implement
    [Device\_Settings](/wiki/Device_Settings "wikilink") in ICC profiles
    -   changed to ICC meta tag of type dict in v0.1.13

|     |                         |                |                   |                               |
|-----|-------------------------|----------------|-------------------|-------------------------------|
|     | Progress: 100% \[done\] | Target: 0.1.10 | Start: 2008.00.00 | Assigned to: Kai-Uwe Behrmann |
||

-   generalise to Sane, CUPS ... see as well
    [here](/wiki/Device_Settings#Specific_Considerations "wikilink")

|     |                         |                |                   |                                               |
|-----|-------------------------|----------------|-------------------|-----------------------------------------------|
|     | Progress: 100% \[done\] | Target: 0.1.10 | Start: 2009.03.00 | Assigned to: Kai-Uwe Behrmann, Yiannis Belias |
||

-   -   (done) publicise the [device module communication
        protocol](/wiki/Device_Settings#Module_Protocol "wikilink") on a
        separate ColourWiki page

-   (done) integrate into the [KDE
    Kolor-manager](http://code.google.com/soc/2008/openicc/appinfo.html?csaid=9EFC0E521D25020)
    mentored by [OpenICC](/wiki/OpenICC "wikilink") developers

|     |                         |                |                   |                                                                        |
|-----|-------------------------|----------------|-------------------|------------------------------------------------------------------------|
|     | Progress: 100% \[done\] | Target: 0.1.10 | Start: 2008.03.00 | Assigned to: Joe Simon, Hal V. Engel, Cyrille Berger, Kai-Uwe Behrmann |
||

#### Monitor

-   check for validity of a display setup (calibrated: yes/no, expired,
    ...)
-   done (add non EDID monitor support - by a mix of X description and
    by Xinerama geometry (prepared for 0.1.8))

|     |                         |               |                   |                               |
|-----|-------------------------|---------------|-------------------|-------------------------------|
|     | Progress: 100% \[done\] | Target: 0.1.8 | Start: 2007.08.00 | Assigned to: Kai-Uwe Behrmann |
||

-   done (common screen naming scheme for X11, osX and Windows)
-   [Named Colours](#Named_Colours "wikilink") in X11, osX ,Windows
    representation
-   (done) clear about VCGT handling, use Xcalib (licensing?) or
    ArgyllCMS, give at least a hint at configure time “found
    Xcalib/Argyll - can load VCGT” - Oyranos shells out for xcalib
-   (done) support the upcoming [X11 CM
    protocols](http://www.freedesktop.org/wiki/OpenIcc/ColorManagementNearX)
    developed by Tomas Carnecky. implemented in graph but need
    drafting/specification
-   done (XRandR support)
-   (done) support Apples X11

### ICC profile handling

-   check for well behaving of Editing colour spaces (Matrix, RGB: gamma
    equally over all channels, Gray axis, ...)
-   (done) check ICC profiles It is something better suited for
    SampleICC - packaged on OBS.
-   (obsolete) extraction of colorimetric informations from a profile
    like primaries, gamma or profile type

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
| Progress 90% | Version: 0.1.x | Start: 2004 | Assigned to: Kai-Uwe Behrmann |
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
    -   (done) mixed colour space documents for internet warning/quiet
        (OY\_MIXED\_COLOUR\_INTERNET\_DOCUMENT\_WARNING)

<!-- -->

-   rendering intent [(Craig Ringer's
    suggestion)](http://lists.freedesktop.org/archives/openicc/2007q4/000963.html)
    -   Perceptual
    -   Relative Colorimetric with BPC
    -   -- Rarely Needed --
    -   Relative Colorimetric without BPC
    -   Absolute Colorimetric
    -   Saturation
    -   BPC affect all RIs; a Relative Colorimetric with BPC can only be
        used for convenience
    -   implement like a skin?
    -   Where to translate the general CMS options into the above
        suggested combined options? In the 'oicc' module?
    -   Reference: [AdobeBPC
        spec](http://www.adobe.com/devnet/photoshop/sdk/AdobeBPC.pdf)

<!-- -->

-   allow non persistent settings, examples:
    -   (done) useful for temporarily adding profile paths in osX
        bundles - paths follow the OpenICC spec through XDG\_DATA\_DIRS
    -   switching default profiles to gamma 1.0 versions in one
        application, without touching other applications

#### Directory Paths

-   [OpenICC path specification](/wiki/OpenIccDirectoryProposal "wikilink")

|                |                |                     |                   |
|----------------|----------------|---------------------|-------------------|
| Progress: 100% | Version: x.x.x | Start: defacto 2004 | Assigned to: open |
||

-   (obsoleted by XDG variables) ICC\_PROFILE\_PATH ? how to interact
    with Oyranos
-   (done) update Oyranos' internal path representation to the [OpenICC
    Directory Proposal](/wiki/OpenIccDirectoryProposal "wikilink")
-   (done) OY\_MODULE\_PATHS for CMM's
-   (done) update to v0.2

### Default Profiles

-   (done) naming of ECI profiles to something FOGRA corresponding
    (Chris Murphy and others on OpenICC)
-   (done) most ECI profiles are replaced with Argyll created ones
-   (done) remains to relicense or replace the eciRGB ones
-   country specific settings

|               |                                            |        |                               |
|---------------|--------------------------------------------|--------|-------------------------------|
| Progress: 92% | Version: [0.1.8](#Target_0.1.8 "wikilink") | Start: | Assigned to: Kai-Uwe Behrmann |
||

### CMM Framework

-   back end API a typical CMM should provide
    -   on disk caching
    -   (done) transform caching (file format - device link)

|     |               |                |             |                                          |
|-----|---------------|----------------|-------------|------------------------------------------|
|     | Progress: 75% | Version: x.x.x | Start: 2007 | Assigned to: Kai-Uwe Behrmann (Scribus?) |
||

-   front end API, transforms, caching, image description - buffer
    layout / screen position

|     |               |                |             |                               |
|-----|---------------|----------------|-------------|-------------------------------|
|     | Progress: 80% | Version: 1.x.x | Start: 2007 | Assigned to: Kai-Uwe Behrmann |
||

-   [Oyranos/Null Transform
    Checking](/wiki/Oyranos/Null_Transform_Checking "wikilink") - implicite;
    beside explicite opt out support in options

|     |              |                |             |                |
|-----|--------------|----------------|-------------|----------------|
|     | Progress: 0% | Version: 1.x.x | Start: 2008 | Assigned to: ? |
||

-   -   options handling (xml, GUI)
        -   (done) static options should be displayed to users according
            to preferences (for instance [mismatch
            option](/wiki/Oyranos_Configuration_Dialog#Colour_Space_Mismatch "wikilink"))

|     |                |                |             |                                   |
|-----|----------------|----------------|-------------|-----------------------------------|
|     | Progress: 100% | Version: x.x.x | Start: 2006 | Assigned to: Kai-Uwe Behrmann + ? |
||

-   -   [Plug-in options / dynamic GUI](/wiki/XML_Plug-in_options "wikilink")

|     |               |                |             |                                                        |
|-----|---------------|----------------|-------------|--------------------------------------------------------|
|     | Progress: 20% | Version: 1.x.x | Start: 2008 | Assigned to: [Marijana](/wiki/Marijana "wikilink") Novakovic |
||

-   file support (tiff,png,jpeg)

|     |               |                              |                   |                               |
|-----|---------------|------------------------------|-------------------|-------------------------------|
|     | Progress: 35% | Version: first use in Colori | Start: 2007-09-10 | Assigned to: Kai-Uwe Behrmann |
||

### Named Colour

-   colour information structure

|               |                                        |                   |                               |
|---------------|----------------------------------------|-------------------|-------------------------------|
| Progress: 60% | Version: first use in ICC Examin v0.45 | Start: 2007-09-03 | Assigned to: Kai-Uwe Behrmann |
||

Constitute a colour patch representation:

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
-   state is shown
    [here](http://www.behrmann.name/wind/oyranos/icc_examin_2007.09.24.html)
-   done - allow for grouping ( swatches )
-   exchange as colour selection(s) in X11, Quartz ...
-   Named Colours (oyNamedColour(s)\_s) &lt;-&gt; data blob (Create's
    colour swatch XML, CGATS, ...) in a plugable fashion
-   keep in sync with
    [Create](http://create.freedesktop.org/wiki/index.php?title=Swatches_-_colour_file_format)
-   HDR range information
-   creator signature?
-   gamut warning with the device, which is exceeded - monitor, printer,
    colour space
-   to sRGB float conversion from Lab(D50)/XYZ or from channels over ICC
    profile with lcms2
-   gamma handling?
-   extra channel handling (scheme for explicitly naming alpha, UV ...)
    enums? string tags? ...

### Miscellaneous

-   done (split Oyranos headers for users, configuration)
-   done (show in headers only stable functions)
-   done (remove unstable functions from descriptions)

<!-- -->

-   (done) later show only advanced options to those users who like it
    -   something like default settings / policy
    -   and modify policy, advanced or custom

<!-- -->

-   done(v0.1.5) Bob Friesenhahn suggested Oyranos should be completely
    relocatable
-   (done) IPC (Xorg, ...?)

Todo
----

[Oyranos](/wiki/Oyranos "wikilink") Roadmap

### Target 2.x.x

-   stable API
    -   graph API - work in progress

<!-- -->

-   add script host (OpenGTL/OpenCL/...)
-   write new renderer for oForms (Qt/Gtk/...)

### Target 1.0.0

-   stable API
    -   settings, profile query - seems a good candidate (oyranos.h +
        oyranos\_icc.h)
    -   device and profile APIs - with the help of the [GSoC2010 code
        refactoring](/wiki/Oyranos/Code_Generator "wikilink")

### Target 0.2.x

-   (done) embed Elektra for easier distribution
-   (done) patch SANE
-   (done) add SANE module
-   clarify image\_display example (FLTK CM policy on osX/native X/...)
-   (done) install compiz plug-in (split out like ICC Examin?)
-   (done) install Xorg tools
-   (done) work with 'meta' tag
-   (done) embed meta tag - in device specific tools like
    oyranos-monitor
    -   use intermediate XML to allow for easy editing let specialised
        tools care about, like SampleICC, or...
    -   (done) couple close to the according driver, e.g. oyX1, oyRE ...
-   (done) split out icc-profiles -
    <http://sourceforge.net/projects/openicc/files/OpenICC-Profiles/>
-   (done) finish lcms2 CMM
    [1](https://sourceforge.net/tracker/?func=detail&aid=3054285&group_id=177017&atid=879553)
-   (done)missed monitor API in doxygen documentation
-   (done)\_ICC\_PROFILE\_IN\_X\_VERSION lost?

### Target 0.1.10

-   (done) [device DB
    framework](/wiki/Device_Settings#Implementation_Details "wikilink")

### Target 0.1.8

-   (done) error handling
-   (done) information callback function:

` int (*callback)(int code, const char* format, ...)`

-   -   internally all can stay with macros
    -   the context should remain distinguishable, as over a pointer or
        a ID, the anonymous callback design above is problematic for OO
        programming

-   override default settings, dependent whether they are inbuild or
    explicitely set by a user
    [2](http://www.behrmann.name/wind/cinepaint/cinepaint_2007.04.13_1.html):
    delayed until options are inside a oyOptions\_s objetc
-   (done) gray profile setting
-   (done) license change as [stated](http://www.oyranos.org/#license)
-   (done) new default profiles from
    [ECI](http://www.eci.org/eci/de/060_downloads.php)
-   (done) investigate in ColorSync ignoring some CMM:SGI marked
    profiles
-   (done) look into newer Elektra library API (Oyranos v0.1.7 can use
    Elektra v0.6.4) v0.1.8 uses Elektra v0.7.x(which waits for its
    release)

### External

-   [Fedora bug
    entry](https://bugzilla.redhat.com/show_bug.cgi?id=239936)

[--&gt; back to Oyranos wiki](/wiki/Oyranos "wikilink")
