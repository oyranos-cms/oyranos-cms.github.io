---
title: DefaultProfile
permalink: wiki/DefaultProfile/
layout: wiki
---

part of [Oyranos](/wiki/Oyranos "wikilink") documentation:

enum oyDEFAULT\_PROFILE

Enumeration values:

`   oyEDITING_RGB   Rgb Editing (Workspace) Profile`  
`   oyEDITING_CMYK  Cmyk Editing (Workspace) Profile`  
`   oyASSUMED_XYZ   standard XYZ assumed source profile`  
`   oyASSUMED_LAB   standard Lab assumed source profile`  
`   oyASSUMED_RGB   standard RGB assumed source profile`  
`   oyASSUMED_CMYK  standard Cmyk assumed source profile`  
`   oyDEFAULT_PROFILE_TYPES     just for easen Gui design`

-   Jan-Peter Homann and Chris Murphy voted to hide Lab and XYZ. If
    there is no practical usage, There seems usage of them in some
    workflows.

<!-- -->

-   older tasks:
    -   done (As discussed on OpenICC INPUT should change to something
        like UNTAGED.)
    -   done (WORKSPACE should become EDITING (Chris Murphy))
    -   done (Jan-Peter Homann requested an differenciation between Cmyk
        and Rgb Editing colour space.)
    -   done (I would change the name of Input INPUT\_CMYK to EDITING
        CMYK (Jan-Peter))

