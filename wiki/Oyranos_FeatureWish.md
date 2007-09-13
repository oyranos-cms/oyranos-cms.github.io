---
title: Oyranos/FeatureWish
permalink: wiki/Oyranos/FeatureWish/
layout: wiki
tags:
 - Oyranos
---

### Feature Wishes for [Oyranos](/wiki/Oyranos "wikilink")

They come mostly from discussions at the [OpenICC](/wiki/OpenICC "wikilink")
email list.

-   check for validity of a display setup (calibrated: yes/no, expired,
    ...)

<!-- -->

-   check for well behaving of Editing colour spaces (Matrix, RGB: gamma
    equally over all channels, Gray axis, ...)

<!-- -->

-   use of standard folders for: display profiles, RGB editing profiles,
    CMYK editing profiles.

If advanced users want to use special profiles e.g. for editing, they
have manually to add the profile to this folder. This is an easy way to
implement a solution, that beginners are not able to choose wrong
profiles by accident.

-   color management policies
    -   done (only allow flat color documents or allow mixed mode
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

<!-- -->

-   ICC\_PROFILE\_PATH ? how to interact with Oyranos

<!-- -->

-   allow non persistent settings, examples:
    -   useful for temporarily adding profile paths in osX bundles
    -   switching default profiles to gamma 1.0 versions in one
        application, without touching other applications

<!-- -->

-   naming of ECI profiles to something FOGRA corresponding (Chris
    Murphy and others on OpenICC)

<!-- -->

-   add non EDID monitor support - by a mix of X description and by
    Xinerama geometry (prepared for 0.1.8)

| Named Colour information structure |
|------------------------------------|
| Progress 20%                       |
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
-   allow for grouping
-   exchange in X11, Quartz ...
-   keep in sync with
    [Create](http://create.freedesktop.org/wiki/index.php?title=Swatches_-_colour_file_format)

