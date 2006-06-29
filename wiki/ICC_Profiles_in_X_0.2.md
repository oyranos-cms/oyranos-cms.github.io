---
title: ICC Profiles in X 0.2
permalink: wiki/ICC_Profiles_in_X_0.2/
layout: wiki
tags:
 - Oyranos
---

The original specification is found on Ross Burtons side: [ICC Profiles
In X
Specification](http://www.burtonini.com/computing/x-icc-profiles-spec-0.1.html).
Here you find a modified version of the above. The below text is just a
proposal.

### \_ICC\_PROFILE

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

[--&gt; back](/wiki/Oyranos "wikilink")
