---
title: ICC Profiles in X Specification 0.3
permalink: wiki/ICC_Profiles_in_X_Specification_0.3/
layout: wiki
tags:
 - Oyranos
 - Standards
---

<h1>
DRAFT

</h1>
| Revision History                                                                |
|---------------------------------------------------------------------------------|
| [Revision 0.1](http://www.burtonini.com/computing/x-icc-profiles-spec-0.1.html) |
| [Revision 0.2](http://www.burtonini.com/computing/x-icc-profiles-spec-0.2.html) |
| Draft 1 for Revision 0.3                                                        |
||

Introduction
------------

This is a specification for associating ICC colour profiles with X
monitors. With this specification applications can obtain the
appropriate display profile for the monitor they are interessted in, and
apply colour correction to any images, which are being shown to the
user.

Specification
-------------

Currently there is only one atom base name defined.

\_ICC\_PROFILE
--------------

The atom name for the first monitor in a root window is \_ICC\_Profile.

For root windows spanning more than one monitor, as typical in Xinerama
multihead configurations, a atom for each monitor is added holding the
appropriate ICC profile. The first monitor uses the \_ICC\_Profile atom
name. All monitors in a root window starting from number one use
\_ICC\_Profile as atom name extended with an underscore plus the monitor
number, e.g. \_ICC\_Profile\_1 . Monitor counting starts with zero. Thus
a \_ICC\_Profile\_0 atom should not appear.

The atoms are of type <span class="type">XA\_CARDINAL</span> with 8-bit
elements. The value of the atom should be a literal ICC profile, that
applications can read and parse directly.

This property does not have to be set on every monitor. When this
property is not set for a monitor, this monitor is uncharacterised, and
colour correction for this monitor should be done using the sRGB colour
space.

As profiles can be large, applications should read the profile for a
particular screen once, and cache it. As a screen's profile may change
during the lifetime of the progress, applications should ask to receive
property change notifications from the root window, even if they don't
currently have a profile set. Applications which can change screens
using mechanisms such as display migration should be aware that the new
screen is likely to have different profiles assigned to monitors.

\_ICC\_PROFILE\_IN\_X\_VERSION
------------------------------

The \_ICC\_PROFILE\_IN\_X\_VERSION atom specifies the version of this
specification applied. To simplify parsing the minor revision number is
multiplied by 1 plus the major number by 100. So for example revision
0.3 would result in:  
0\*100 + 3\*1 =&gt; 3

References
----------

1. [International Color Consortium](http://www.color.org)

2. [Ross Burtons
page](http://www.burtonini.com/computing/x-icc-profiles-spec-latest.html)

2007 © Kai-Uwe Behrmann

[back --&gt; Oyranos](/wiki/Oyranos "wikilink") or [Oyranos X11
Requirements](/wiki/Oyranos_X11_Requirements "wikilink")
