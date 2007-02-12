---
title: ICC Profiles in X Specification 0.2
permalink: wiki/ICC_Profiles_in_X_Specification_0.2/
layout: wiki
tags:
 - Oyranos
---

| Revision History                                                                |
|---------------------------------------------------------------------------------|
| [Revision 0.1](http://www.burtonini.com/computing/x-icc-profiles-spec-0.1.html) |
| Revision 0.2                                                                    |
||

Introduction
------------

This is a specification for associating ICC colour profiles with X
screens. With this specification applications can obtain the appropriate
display profile for the screen they are on, and apply colour correction
to any images which are being shown to the user.

Specification
-------------

Currently there is only one atom base name defined.

\_ICC\_PROFILE
--------------

The atom name for the first screen in a root window is \_ICC\_Profile.

For root windows spanning more than one screen, as typical in Xinerama
multihead configurations, a atom for each screen is added holding the
appropriate ICC profile. All screens in a root window starting from
number one use \_ICC\_Profile as atom name extended with an underscore
plus the screen number, e.g. \_ICC\_Profile\_1 .

The atoms are of type <span class="type">XA\_CARDINAL</span> with 8-bit
elements. The value of the atom should be a literal ICC profile, that
applications can read and parse directly.

This property does not have to be set on every screen. When this
property is not set on a screen, the screen is uncalibrated, and no
colour correction for display should be done.

As profiles can be large applications should read the profile for a
particular screen once, and cache it. As a screen's profile may change
during the lifetime of the progress, applications should ask to receive
property change notifications from the root window, even if they don't
currently have a profile set. Applications which can change screens
using mechanisms such as display migration should be aware that the new
screen is likely to have a different profile.

References
----------

1. [International Color Consortium](http://www.color.org)

2. [Revision 0.1 of this
specification](http://www.burtonini.com/computing/x-icc-profiles-spec-0.1.html)

2006 © Kai-Uwe Behrmann

[back --&gt; Oyranos](/wiki/Oyranos "wikilink")
