---
title: ICC Profiles in X Specification 0.4
permalink: wiki/ICC_Profiles_in_X_Specification_0.4/
layout: wiki
tags:
 - Oyranos
 - Standards
---

<h1>
DRAFT

</h1>
<table>
<thead>
<tr class="header">
<th><p>Revision History</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="http://www.burtonini.com/computing/x-icc-profiles-spec-0.1.html">Revision 0.1</a></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.burtonini.com/computing/x-icc-profiles-spec-0.2.html">Revision 0.2</a></p></td>
</tr>
<tr class="odd">
<td><p>Draft 1 for Revision 0.3</p></td>
</tr>
<tr class="even">
<td><p>Draft 2 for Revision 0.3</p></td>
</tr>
<tr class="odd">
<td><p>Draft 1 for Revision 0.4</p></td>
</tr>
<tr class="even">
</tr>
</tbody>
</table>

Introduction
------------

This is a specification for associating ICC colour profiles with X
monitors. With this specification applications and services can obtain
the appropriate display profile for the monitor they are interessted in,
and apply colour correction to any images, which are being shown to the
user.

Specification
-------------

The \_ICC\_PROFILE base name contains the literal ICC colour profile. A
atom with name \_ICC\_PROFILE\_IN\_X\_VERSION tells about awareness of
the setting application or service. The \_ICC\_PROFILE\_SETUP\_LOCK atom
is intented for locking in dynamic changing environments, especially for
the setup application or service. The \_ICC\_PROFILE\_SETUP atom allowes
for finding out whether a configuration is up to date.

\_ICC\_PROFILE
--------------

The atom name for the first monitor in a root window is \_ICC\_PROFILE.

For root windows spanning more than one monitor, as typical in Xinerama
and XRandR multihead configurations, a atom for each monitor is added
holding the appropriate ICC profile. The first monitor uses the
\_ICC\_PROFILE atom name. All monitors in a root window starting from
number one use \_ICC\_PROFILE as atom name extended with an underscore
plus the monitor number, e.g. \_ICC\_PROFILE\_1 . Monitor counting
starts with zero. Thus a \_ICC\_PROFILE\_0 atom should not appear.

The atoms are of type <span class="type">XA\_CARDINAL</span> with 8-bit
elements. The value of the atom should be a literal ICC profile, that
applications can read and parse directly.

This property does not have to be set on every monitor. When this
property is not set for a monitor, this monitor is uncharacterised, and
colour correction for this monitor should be done using the sRGB colour
space.

As profiles can be large, applications should read the profile for a
particular screen once, and cache it. As a screen's profile may change
during the lifetime of the process, applications should ask to receive
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
The atom should be stored as ascii text of type
<span class="type">XA\_CARDINAL</span> with 8-bit elements.

\_ICC\_PROFILE\_SETUP\_LOCK
---------------------------

A application or service, which is able to setup the \_ICC\_PROFILE
atom(s), may obtain notification for a server configuration change, e.g.
after dynamically connecting a new monitor. Then this service can try to
evaluate the configuration and update appropriately. First a lock has to
be set with the atom name \_ICC\_PROFILE\_SETUP\_LOCK. The content of
this atom should contain the actual service PID and time() value. The
string value should be:  
“pid:time”, e.g. “293:1231432919”.  
The atom should be stored as ascii text of type
<span class="type">XA\_CARDINAL</span> with 8-bit elements.  
After the X server is configured again the \_ICC\_PROFILE\_SETUP\_LOCK
should be removed by the the locking service.

\_ICC\_PROFILE\_SETUP
---------------------

The atom with name \_ICC\_PROFILE\_SETUP should be set by the
configuring service. The content of this atom should contain the actual
service PID and time() value. The string value should be:  
“pid:time”, e.g. “293:1231432919”.  
The atom should be stored as ascii text of type
<span class="type">XA\_CARDINAL</span> with 8-bit elements.

**(How does a client know that a configuration is invalid? output count?
regular check every 10 seconds?)**

References
----------

1. [International Color Consortium](http://www.color.org)

2. [central specification
host](http://www.freedesktop.org/wiki/Specifications/icc_profiles_in_x_spec)
@ freedesktop.org

2005 © Ross Burton; 2006-2009 © Kai-Uwe Behrmann

[back --&gt; Oyranos](/wiki/Oyranos "wikilink") or [Oyranos X11
Requirements](/wiki/Oyranos_X11_Requirements "wikilink")
