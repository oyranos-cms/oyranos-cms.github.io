---
title: ICC meta Tag for Monitor Profiles 1.0
permalink: wiki/ICC_meta_Tag_for_Monitor_Profiles_1.0/
layout: wiki
tags:
 - Standards
---

| Revision History |            |
|------------------|------------|
| Revision 1.0     | 2012-01-29 |
||

Introduction
------------

The specification provides means to embed monitor information into ICC
profiles.

ICC profile vendors have to maintain different installation procedures
to register ICC device profiles on a client machine. This is either
fully customised, but only for certain operating systems, or an manual
error prone task through the required user interaction. With ICC
profiles for monitors containing device information, it will be easy for
colour management systems to identify monitors and use a matching ICC
profile without special registration in the system. This allows for easy
preselection and implicit configuration. The advantage for vendors are
less maintenance costs and better cross platform support in a flexible
manner. Users benefit by the implementation of this proposal through a
simplified and more robust colour management system. Adding of device
information to ICC profiles can be assisted through according tools.

This proposal defines key/value pairs for storing into a ICC display
profiles meta tag. Consequently only colour management and device
identification related properties are considered for inclusion. A
explicit configuration in a given CMS shall override such implicit
mechanisms as defined by this proposal.

Specification
-------------

This version is based on the
[OpenICC\_Configuration\_0.1](/wiki/OpenICC_Configuration_0.1 "wikilink").

### Keys

The following key/value pairs are defined

-   (key: value)
-   EDID\_mnft: decoded three byte string from EDID address 8-9
-   EDID\_manufacturer: mapping of mnft to a full string - only for
    displaying
-   EDID\_mnft\_id: MSB decoded numerical representation of EDID address
    8-9
-   EDID\_model\_id: LSB decoded numerical representation of EDID
    address 10-11
-   EDID\_date: decoded year of production from EDID address 17 and week
    of production from EDID address 16
-   EDID\_red\_x:
-   EDID\_red\_y:
-   EDID\_green\_x:
-   EDID\_green\_y:
-   EDID\_blue\_x:
-   EDID\_blue\_y:
-   EDID\_white\_x:
-   EDID\_white\_y:
-   EDID\_gamma:

The *EDID\_\[red,green,blue,white\]\_* prefixed keys and *EDID\_gamma*
contain floats with decimal point. The values are decoded from EDID
address 25-34 (colour primaries) plus address 23 (gamma).

-   EDID\_model: decoded string from EDID text section 54 till 125 of
    typical type 252
-   EDID\_serial: decoded string from EDID text section 54 till 125 of
    typical type 255

Detailed instructions how to decode EDID can be obtained from VESA
through the Enhanced Extended Display Identification Data Standard
(E-EDID) - Rel. A, 1.0 .

A parser must be prepared to interpret the contained values numerically
and not always textual as is otherwise preferred.

### Example

` {`  
`   `“`org`”`: {`  
`     `“`freedesktop`”`: {`  
`       `“`openicc`”`: {`  
`         `“`device`”`: {`  
`           `“`monitor`”`: {`  
`             `“`prefix`”`: `“`EDID_`”`,`  
`             `“`EDID_red_y`”`: `“`0.339844`”`,`  
`             `“`EDID_red_x`”`: `“`0.639648`”`,`  
`             `“`EDID_mnft_id`”`: `“`7789`”`,`  
`             `“`EDID_blue_x`”`: `“`0.144531`”`,`  
`             `“`EDID_manufacturer`”`: `“`Goldstar`` ``Company`` ``Ltd`”`,`  
`             `“`EDID_green_y`”`: `“`0.615234`”`,`  
`             `“`EDID_green_x`”`: `“`0.290039`”`,`  
`             `“`EDID_white_y`”`: `“`0.329102`”`,`  
`             `“`EDID_white_x`”`: `“`0.313477`”`,`  
`             `“`EDID_date`”`: `“`2007-T5`”`,`  
`             `“`EDID_gamma`”`: `“`2.2`”`,`  
`             `“`manufacturer`”`: `“`Goldstar`` ``Company`` ``Ltd`”`,`  
`             `“`mnft`”`: `“`GSM`”`,`  
`             `“`EDID_blue_y`”`: `“`0.0703125`”`,`  
`             `“`EDID_mnft`”`: `“`GSM`”`,`  
`             `“`EDID_model`”`: `“`L203WT`”`,`  
`             `“`model`”`: `“`LG`` ``Flatron`` ``L203W`”`,`  
`             `“`EDID_model_id`”`: `“`20030`”  
`           }`  
`         }`  
`       }`  
`     }`  
`   }`  
` }`

Discussion
----------

A tag to embed the complete EDID data block is defined. But that serves
different goals. Namely it is not possible to support a wider range of
devices by this approach.

To create a generic meta tag, the serial number and possibly production
times need to be stripped from the meta tag, if they are considered non
relevant in regards of colour rendering. Most monitors series will be
well identified by the EDID\_model\_id and EDID\_mnft\_id entries.
Others might need the colorimetric primaries and gamma if they can
switch colour spaces.

The “EDID\_date”, “EDID\_mnft\_id” and “EDID\_model\_id” keys might
contain value ranges as allowed by the ICC meta tag definition.

Numeric matching of tags depends precision as allowed by the EDID
specification. As a informal hint, a delta of +-0.0005 might be good
enough to match colorimetry origin from EDID.

References
----------

1. ICC - <http://www.color.org/>

2. meta tag -
<http://www.color.org/ICCSpecRevision_25-02-10_dictType.pdf>

3. VESA - <http://www.vesa.org/>

4. EDID - Enhanced Extended Display Identification Data Standard
(E-EDID) - Rel. A, 1.0

4.1 <http://en.wikipedia.org/wiki/EDID> (overview)

5. ISO 8601 - Data elements and interchange formats – Information
interchange – Representation of dates and times

Changes
-------

-   [DRAFT
    1](http://lists.freedesktop.org/archives/openicc/2010q4/002273.html) -
    initial
-   [DRAFT
    2](http://lists.freedesktop.org/archives/openicc/2010q4/002283.html) -
    use EDID\_ prefix, Max Derhack and Lars Borg, use ISO 8601 for
    dates, Lars Borg, splitting of colorimetry compound, Richard Hughes
-   [DRAFT
    3](http://lists.freedesktop.org/archives/openicc/2010q4/002293.html) -
    remove redundant key name parts, synchronise names
-   [DRAFT
    4](http://lists.freedesktop.org/archives/openicc/2011q4/004431.html) -
    use JSON example
-   [DRAFT
    5](http://lists.freedesktop.org/archives/openicc/2012q1/004460.html) -
    correct JSON example, as pointed out by Florian Höch
-   [1.0](http://lists.freedesktop.org/archives/openicc/2012q1/004556.html) -
    add hint about error delta, clarify colorimetric prefixes

2010-2012 © Kai-Uwe Behrmann
